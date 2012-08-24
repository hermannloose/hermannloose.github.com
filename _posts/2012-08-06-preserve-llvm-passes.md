---
layout: post
title: LLVM passes, thou shalt preserve them!
meta:
  description: A short blog post about misleading assertions and shooting
      yourself in the foot with dependencies between LLVM passes.
tags:
  - english
  - programming
lastmod: 2012-08-24T23:00:00+02:00
---

I am currently working on some LLVM passes for my intermediate thesis aka
*Großer Beleg* at university and I came across an annoying problem this
morning, due to a somewhat misleading assertion message in LLVM's PassManager.

I have a large ModulePass, that does some inspection across functions, keeps
global state and can thus not comfortably be a FunctionPass. Within it
I require two FunctionPasses

{% highlight cpp %}
void SomeModulePass::getAnalysisUsage(AnalysisUsage &AU) const {
  AU.addRequired<FirstFunctionPass>();
  AU.addRequired<SecondFunctionPass>();
}
{% endhighlight %}

and later call them in `ModulePass::runOnModule(Module &M)`:

{% highlight cpp %}
// function is a Module::iterator
FirstFunctionPass &FFP = getAnalysis<FirstFunctionPass>(*function);
SecondFunctionPass &SFP = getAnalysis<SecondFunctionPass>(*function);
{% endhighlight %}

This kept failing on me—precisely after executing both required passes on the
correct function just fine, mind you—with a rather cryptic

```
Assertion 'ResultPass && "Unable to find requested analysis info"' failed.
```

Which after a lot of cursing and random debugging attempts turned out to be
simply due to the second function pass invalidating the first function pass,
because I did not add it to the second pass's *preserved set*, to inform the
PassManager that these two actually don't care about each other.

{% highlight cpp %}
void SecondFunctionPass::getAnalysisUsage(AnalysisUsage &AU) const {
  AU.addPreserved<FirstFunctionPass>();
}
{% endhighlight %}

I was aware of the performance implications of not specifying preserved passes,
just not the fact that it would produce weird results like this. Trivial
problem, lots of time wasted because the assertion wasn't pointing me in the
right direction—*I know I'm whining on a pretty high level here, in general
LLVM does an awesome job at telling me where exactly I'm being stupid*—and
there seems to be no runtime checking for "impossible" situations like this.

(There might be just among FunctionPasses if I remember correctly, but it seems
that requiring things from within a ModulePass, you're out of luck right now.
Also, when I request `--debug-pass=Structure` it does not prefix "results known
to be dead" as [mentioned
here](http://llvm.org/docs/WritingAnLLVMPass.html#interaction), unfortunately.
Was this taken out?)

Hope this helps one or two people searching for answers to the same problem.
