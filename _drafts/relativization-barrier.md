---
title: The relativization barrier
date: 2019-12-24 00:04 -0500
tags: [tcs, complexity-theory]
---

# The relativization barrier

In this post, I want to highlight a famous result of Baker, Gill, and Solovay from 1975 that establishes a theoretical obstacle to resolving the $$\mathbf{P}$$ vs. $$\mathbf{NP}$$ problem. Concretely, their result shows that a large class of proof techniques which possess a certain property cannot be used to show that $$\mathbf{P} \subsetneq \mathbf{NP}$$ (or $$\mathbf{P} = \mathbf{NP}$$, for that matter). This property is called *relativization*, and this obstacle is therefore termed the *relativization barrier*. I will first outline a theorem (the *time hierarchy theorem*) whose proof indeed relativizes, and define relativization and other relevant notions; then, I will sketch the argument of Baker, Gill, and Solovay that shows that no relativizing proof can resolve the $$\mathbf{P}$$ vs. $$\mathbf{NP}$$ problem. My main references for this material are Chapter 3 of [Arora and Barak's *Complexity Theory: A Modern Approach*](http://theory.cs.princeton.edu/complexity/diagchap.pdf) and [Aaronson's *P vs. NP*](https://www.scottaaronson.com/papers/pnp.pdf).

### The halting problem

In complexity theory, if $$A$$ and $$B$$ are complexity classes and it is known that $$A \subset B$$, a *separation* is the result that $$A \subsetneq B$$. Most important problems in complexity theory boil down to proving a separation (or equality) between classes. The "original" separation result is due to Alan Turing (contemporaneously with the actual definition of Turing machines themselves). In modern language, Turing separated the classes $$\mathbf{R}$$, the class of all *computable* functions, and $$\mathbf{U}$$, the class of all functions (I am making the latter notation up). This separation is *constructive*: He showed that a particular function is in $$\mathbf{U}$$ but not $$\mathbf{R}$$. This function is the *halting problem* $$HALT$$, which on input a program $$M$$ and a string $$x$$, returns $$1$$ if $$M$$ halts on input $$x$$, and otherwise $$0$$.

How can we show that $$HALT \not\in \mathbf{R}$$? There's a beautiful and short proof by contradiction. Suppose that $$HALT$$ is computable by some program $$A$$. Then consider the following program $$B$$ (in Pythonic pseudocode):

{% highlight python %}
def B(M):
	if A(M, M):          # M halts on input M
		loop_forever()
	else:                # M loops forever on input M
		return 0
{% endhighlight %}

Then what is $$B(B)$$? If $$B(B) = 0$$, then the `else` branch was taken, so $$A(B, B) = 0$$, and so $$B$$ does not halt on input $$B$$. If $$B(B)$$ loops forever, then $$A(B, B) = 1$$, and so $$B$$ does halt on input $$B$$. ($$B(B)$$ cannot return $$1$$.) This is a contradiction, and so $$A$$ cannot exist in the first place!

### The time hierarchy theorem

The above argument is an example of a *diagonalization argument*. As Arora and Barak point out, the central ideas are to represent programs as strings, use programs to simulate other programs, and define a particular program that "outsmarts" the other programs. But we can achieve much more than just showing the uncomputability of the halting problem using this argument. One major consequence is the *time hierarchy theorem*, which is as follows. For any ["computationally nice"](https://en.wikipedia.org/wiki/Constructible_function) function $$f : \mathbb{N} \to \mathbb{N}$$ (roughly any $$f$$ that can be computed by a Turing machine), $$\mathbf{TIME}(f(n)) \subsetneq \mathbf{TIME}(f(n) \log n)$$, where $$\mathbf{TIME}(g(n))$$ denotes the functions that can be computed by programs running in time $$g(n)$$.

One immediate consequence of this theorem are that $$\mathbf{TIME}(n) \subsetneq \mathbf{TIME}(n^2)$$; that is, there are some functions that can be solved using quadratic-time algorithms but not linear-time algorithms. Another is that $$\mathbf{P} \subsetneq \mathbf{EXP}$$ (this is a corollary of the fact that there is a problem in $$\mathbf{TIME}(n^{\log n} \log n) \setminus \mathbf{TIME}(n^{\log n})$$).

A full, formal proof is given in [Chapter 12 of the CS 121 textbook](https://introtcs.org/public/lec_11_running_time.html) but requires several technical details. Here, we will sketch, as in Arora and Barak, the proof that $$\mathbf{TIME}(n) \subsetneq \mathbf{TIME}(n^2)$$. 

**TODO THIS**

This argument actually extends naturally to give a more general separation: It implies, for instance, that $$\mathbf{TIME}(n) \subsetneq \mathbf{TIME}(n^2)$$ (where $$n$$ is the length of the input to a function or program, and $$\mathbf{TIME}(f(n))$$ denotes the set of functions with algorithms running in time $$f(n)$$). The key is to consider the function $$HALT_{n^2}$$, which on input a program $$M$$ and a string $$x$$, returns $$1$$ if $$M$$ halts on input $$x$$ *within $$n^2$$ steps*, and otherwise $$0$$.

Firstly, we claim that $$HALT_{n^2} \not\in \mathbf{TIME}(n)$$. Again, if it were computable by some algorithm $$A$$ running in time $$n$$, we could define an algorithm $$B$$ as above. If $$B(B) = 0$$, then $$A(B, B) = 0$$, so $$B$$ does not halt on input $$B$$ within $$n^2$$ steps, which is impossible since $$n^2 > n$$ and $$B$$ has running time $$n$$. 


. However, this function is in $$\mathbf{TIME}(n^2)$$, since we can just simulate a program $$M$$ on its input $$x$$ 

### Oracles and the relativization barrier

One final notion that's important for this discussion is the notion of an $$f$$-*oracle program* for a function $$f : \{0,1\}^* \to \{0,1\}$$. This is just a program that gets an "oracle" that can compute $$f$$ instantly, and can call this oracle whenever and as many times as it wants. ($$f$$ can be arbitrarily hard, even uncomputable.) We can define *oracle classes* such as $$\mathbf{P}^f$$ and $$\mathbf{NP}^f$$ which represent problems that can be efficiently solved by $$f$$-oracle programs and efficiently verified by $$f$$-oracle programs, respectively. A separation $$A \subsetneq B$$ is said to *relativize* if for all $$f$$, $$A^f \subsetneq B^f$$. (The same could be said of an equality $$A = B$$.) Note that time hierarchy theorem relativizes since the proof is invariant to the presence of an oracle (check it carefully **say something**!). Thus, e.g., $$\mathbf{P}^f \subsetneq \mathbf{EXP}^f$$ for all functions $$f$$. Might we hope for some similar type of result for $$\mathbf{P}$$ and $$\mathbf{NP}$$?

A surprising result of Baker, Gill, and Solovay from 1975 is that the relationship between $$\mathbf{P}$$ and $$\mathbf{NP}$$ does not relativize! In other words, there exists oracles $$f$$ and $$g$$ such that $$\mathbf{P}^f = \mathbf{NP}^f$$ but $$\mathbf{P}^g \neq \mathbf{NP}^g$$. I will sketch what these oracles are below in more detail (this requires some knowledge of complexity theory), but firstly, let's discuss the consequences. This makes $$\mathbf{P}$$ and $$\mathbf{NP}$$ harder to separate (or prove equal) because they must be *sensitive* to the presence of oracles. Intuitively, this means that it isn't enough to just base the arguments off of simulating arbitrary programs, treating them as black boxes. Somehow, a proof that $$\mathbf{P} \subsetneq \mathbf{NP}$$ would have to "inspect the contents" of programs. This obstacle to solving the $$\mathbf{P}$$ vs. $$\mathbf{NP}$$ problem is called the *relativization barrier*. Here is an excerpt from Arora and Barak's discussion which sums it up well:

> [Let us consider] any technique that relies upon the following properties of Turing machines: I) The existence of an effective representation of Turing machines by strings, and II) The ability of one TM to simulate any another without much overhead in running time or space. Any argument that only uses these facts is treating machines as black boxes: the machine’s internal workings do not matter. We [have shown] a general way to define a variant of Turing Machines [i.e., programs] called oracle Turing Machines that still satisfy the above two properties. However, one way of defining the variants results in TMs for which $$\mathbf{P} = \mathbf{NP}$$, whereas the other way results in TMs for which $$\mathbf{P} \subsetneq \mathbf{NP}$$. We conclude that to resolve $$\mathbf{P}$$ versus $$\mathbf{NP}$$ we need to use some other property besides the above two.

Aaronson adds an interesting logical perspective:

> If relativization seems too banal, the way to appreciate it is to try to invent techniques, for proving inclusions or separations among complexity classes, that fail to relativize. It’s harder than it sounds! A partial explanation for this was given by Arora, Impagliazzo, and Vazirani, who reinterpreted the relativization barrier in logical terms. From their perspective, a relativizing proof is simply any proof that "knows" about complexity classes, only through axioms that assert the classes' closure properties, as well as languages that the classes do contain. (For example, $$\mathbf{P}$$ contains the empty language; if $$L_1$$ and $$L_2$$ are both in $$\mathbf{P}$$, then so are Boolean combinations like $$\overline{L_1}$$ and $$L_1 \cap L_2$$.) These axioms can be shown to imply statements such as $$\mathbf{P} \subsetneq \mathbf{EXP}$$. But other statements, like $$\mathbf{P} \subsetneq \mathbf{NP}$$, can be shown to be independent of the axioms, by constructing models of the axioms where those statements are false. One constructs those models by using oracles to "force in" additional languages --- such as $$\mathbf{PSPACE}$$-complete languages, if one wants a world where $$\mathbf{P} = \mathbf{NP}$$ --- which the axioms might not require to be contained in complexity classes like $$\mathbf{P}$$ and $$\mathbf{NP}$$, but which they don't prohibit from being contained, either. The conclusion is that any proof of $$\mathbf{P} \subsetneq \mathbf{NP}$$ will need to appeal to deeper properties of the classes $$\mathbf{P}$$ and $$\mathbf{NP}$$, properties that don't follow from these closure axioms.

Finally, so what actually are the functions $$f$$ and $$g$$?

Intuitively, $$f$$ is a problem that's so hard that once you can solve it, $$\mathbf{P}$$ and $$\mathbf{NP}$$ become the same. The classic example is a complete problem for the class $$\mathbf{PSPACE}$$, which contains all problems that are solvable in *polynomial space*. An example of such a problem is the *true quantified Boolean formula* problem $$TQBF$$, where the goal is to compute whether an arbitrary quantified Boolean formula is true (e.g., $$\exists x_1 \forall x_2 \exists x_3 \forall x_4 \cdots \exists x_{2n-1} \forall x_{2n} \; \varphi(x_1, \ldots, x_{2n+1}))$$ for some Boolean formula $$\varphi$$ in the variables $$x_1, \ldots, x_{2n+1}$$). Then $$\mathbf{NP}^f \subset \mathbf{NPSPACE}$$. the class of all problems that can be verified using polynomial space. By [Savitch's theorem](https://en.wikipedia.org/wiki/Savitch's_theorem), $$\mathbf{NPSPACE} = \mathbf{PSPACE}$$. Then finally, since $$f$$ is $$\mathbf{PSPACE}$$-complete, $$\mathbf{PSPACE} \subset \mathbf{P}^f$$. Thus, $$\mathbf{NP}^f \subset \mathbf{P}^f$$ and so they are equal (the reverse inclusion is trivial).

 In order to pass it, we need proof techniques that don't relativize, which are already hard to come by! Furthermore, unfortunately, there are other known barriers, such as the *natural proofs barrier*, that I would like to address in future posts.