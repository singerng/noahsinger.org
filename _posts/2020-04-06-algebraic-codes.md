---
title: Encoding and decoding algebraic codes
date: 2020-04-06 17:13 -0400
tags: [tcs, error-correcting-codes]
---

# Algebraic codes

This semester, I have been really fortunate to be able to take Prof. Madhu Sudan's class <a href="http://people.seas.harvard.edu/~madhusudan/courses/Spring2020/">CS 229R</a> on error-correcting codes. It's been a great class, although it has unfortunately been cut short in-person by the pandemic. I thought I'd write a post to give a taste of the types of arguments and analyses we've been using.

The fundamental problem in error-correcting codes is to figure out how to encode messages with "redundancy", so that if we transmit the message over a noisy channel (e.g., one that randomly corrupts bits of the transmission), the recipient is still able to recover the message. One of the really cool aspects of the theory of error-correcting codes is that interesting codes arise can be constructed with ideas from many different areas, such as algebra, graph theory, combinatorics, and information theory.

Below, we formally define the fundamental goal of a standard error-correcting code and describe one way to efficiently achieve it using an algebraic construction. An excellent reference on this material is the draft of the [*Essential Coding Theory*](https://cse.buffalo.edu/faculty/atri/courses/coding-theory/book/index.html) book cowritten by Madhu along with Venkatesan Guruswami at CMU and Atri Rudra at Buffalo. My exposition below is derived directly from my class notes and the book; all credit for the material and notation goes to them.

### Introduction and motivations

The basic goal is to build an efficient algorithm to transform a string $$x$$ into an encoded string $$E(x)$$ such that the following are true:

1. $$E(x)$$ is not "much longer" than $$x$$.
3. If $$y$$ is a received copy of $$E(x)$$ with "a few" errors, it should still be possible to *uniquely* decode $$y$$ back to $$x$$.
4. If $$y$$ is a received copy of $$E(x)$$ with "a few" errors, it should still be possible to *efficiently* decode $$y$$ back to $$x$$.

{% include image.html src="posts/figures/ecc-basics.jpeg" caption="The string \"Hello\" encoded with a threefold repetition code, as described below. All but one character of the initial string can be recovered." %}

Formally, from a combinatorial perspective, given some finite alphabet $$\Sigma$$ (for instance, the binary alphabet $$\{0,1\}$$), an *error-correcting code* is a map $$E : \Sigma^k \to \Sigma^n$$. Each string in the image of $$E$$ is called a *codeword*; the code can equivalently be viewed as $$\mathcal{C} := E(\Sigma^k)$$, the collection of all codewords.

There are two fundamental quantitative properties of error-correcting codes, the *rate* $$R := k/n$$ and the *distance* $$d$$, which is defined as $$d := \operatorname{argmin}_{x \neq y \in \mathcal{C}} \Delta(x,y)$$, where $$\Delta(x,y)$$ denotes the Hamming distance between two strings $$x,y \in \Sigma^n$$ (i.e., the number of positions in which $$x$$ and $$y$$ differ). In other words, $$d$$ lower-bounds the distance between any pair of unique codewords. Now if $$E(x)$$ is corrupted into $$y$$ with fewer than $$d/2$$ errors (i.e., $$\Delta(E(x),y) < d/2$$), then it is always possible to *uniquely* decode $$y$$ to $$E(x)$$. (This follows from the triangle inequality. A useful way of visualizing this is that, if we defined the *Hamming ball* of radius $$t$$ about $$x$$ as $$\text{Ball}(x,t) := \{y \in \Sigma^n : \Delta(x,y) \leq t\}$$, the Hamming balls of radius $$\lfloor d/2-1/2\rfloor$$ around each codeword are disjoint.)

Of course, there are algorithmic properties we want for our codes, in addition to high rate and low distance. In particular, the encoding map $$E$$ should be efficiently computable, and the decoding map (mapping $$y$$ back to $$x$$ when the number of errors is not too large) should be efficiently computable as well.

A particular code with parameters as described above is called an $$(n,k,d)_q$$ code, where $$q = \vert\Sigma\vert$$. A standard basic example is the $$(2t+1)$$-fold repetition code which repeats each character in $$x$$ $$2t+1$$ times (over any alphabet $$\Sigma$$). This is a $$((2t+1)k,k,t)_q$$ code, can you see why? If $$\Sigma=\mathbb{F}_q$$ is a finite field[^fields] and $$E$$ is a *linear* map over $$\mathbb{F}_q$$ (equiv. $$\mathcal{C}$$ is a linear subspace of $$\mathbb{F}_q^n$$), then the code is a *linear code*, denoted $$[n,k,d]_q$$. In the remainder of this article, we will consider a linear code with particularly nice mathematical properties, including efficient error-decoding up to half distance!

### Reed-Solomon codes

A gorgeous idea is to use an *algebraic construction* for error-correcting codes. We will let $$q = n$$ be a prime power, let $$k < n$$, and build an $$[n,k,n-k+1]_q$$-code over $$\mathbb{F}_q$$ (it is in general possible to do this for $$n < q$$, but no more instructive). Let the elements of $$\mathbb{F}_q$$ be $$(\alpha_1,\ldots,\alpha_n)$$. The encoding map is as follows: Given a message $$\vec{x} = (x_0, \ldots, x_{k-1}) \in \mathbb{F}_q^k$$, we define the polynomial $$M_{\vec{x}}(z) = \sum_{i=0}^{k-1} x_i z^i$$, and encode $$\vec{x}$$ to the vector $$\vec{E}(\vec{x}) := (M_{\vec{x}}(\alpha_1),M_{\vec{x}}(\alpha_2),\ldots,M_{\vec{x}}(\alpha_{q-1}),M_{\vec{x}}(\alpha_q))$$. In other words, to encode $$\vec{x}$$, we just evaluate the polynomial $$M_{\vec{x}}$$ at every point in the field $$\mathbb{F}_q$$.

We claim that this code has distance $$n-k+1$$; that is, if $$\vec{x} \neq \vec{y}$$, then $$\vec{E}(\vec{x})$$ and $$\vec{E}(\vec{y})$$ differ in at least $$n-k+1$$ positions: $$\Delta(\vec{E}(\vec{x}),\vec{E}(\vec{y})) > n-k$$.

*Proof.* We will prove the contrapositive. Suppose that $$\vec{E}(\vec{x})$$ and $$\vec{E}(\vec{y})$$ differ in fewer than $$n-k+1$$ positions. Then consider the polynomial $$M_{\vec{x}}-M_{\vec{y}}$$. Suppose that this polynomial is nonzero. It has degree less than $$k$$ (since $$M_{\vec{x}}$$ and $$M_{\vec{y}}$$ both have degree less than $$k$$). At the same time, note that $$\vec{E}(M_{\vec{x}}-M_{\vec{y}}) = \vec{E}(M_{\vec{x}}) - \vec{E}(M_{\vec{y}})$$ contains at least $$n-(n-k)$$ zeros by assumption. But then $$M_{\vec{x}}-M_{\vec{y}}$$ is a nonzero polynomial with $$k$$ zeros but degree less than $$k$$, which is a contradiction.[^mantra] Thus, $$M_{\vec{x}}$$ and $$M_{\vec{y}}$$ are the same polynomial, and so $$\vec{x} = \vec{y}$$ (comparing term-by-term). $$\blacksquare$$

This code is called the *Reed-Solomon code*. At this point, we know that it is an $$[n,k,n-k+1]_q$$-code for arbitrary $$k$$. But just because unique decoding is *possible* (when there are fewer than $$(n-k+1)/2$$ errors) doesn't mean it can be done efficiently. In the next section, I'll describe an algorithm for decoding Reed-Solomon codes.

### The Berlekamp-Welch algorithm

Let us restate the decoding problem as a fully algorithmic problem. In what follows, the notation $$\mathbb{F}_q^{\leq t}[x]$$ means a polynomial in the variable $$x$$ with coefficients in $$\mathbb{F}_q$$ of degree at most $$t$$.

{% capture rs_problem %}
- *Parameters*: Output length $$n$$, input length $$k$$, and number of allowed errors $$t < \frac{n+k-1}2$$.
- *Input*: A sequence $$\vec{y} \in \mathbb{F}_q^n$$.
- *Output*: The (unique) polynomial $$f \in \mathbb{F}_q[x]$$ of degree less than $$k$$ such that $$\Delta(\vec{y},(f(\alpha_1),\ldots,f(\alpha_q))) \leq t$$.
{% endcapture %}
{% include box.html content=rs_problem title="Problem (Reed-Solomon decoding)" %}

In other words, we assume that such $$f$$ (corresponding to the original message $$\vec{x}$$) exists, and our goal is to recover it efficiently. The following algorithm is due to Berlekamp and Welch; (as best I can tell) it was patented in 1983, while the Reed-Solomon code itself was introduced in 1960.

{% capture bw_algorithm %}
1. Find a pair of polynomials $$E \in \mathbb{F}_q^{\leq t}[x], W \in \mathbb{F}_q^{<k+t}[x]$$ such that for all $$i \in \{1,\ldots,q\}$$, $$E(\alpha_i) y_i = W(\alpha_i)$$.
2. Output $$f := W/E$$.
{% endcapture %}
{% include box.html content=bw_algorithm title="Algorithm (Berlekamp-Welch algorithm)" %}

*A priori*, this algorithm might not even be well-defined: Why do we know that such a pair of polynomials $$(W,E)$$ exists? Why must $$E$$ divide $$W$$? How can this be implemented efficiently? To analyze this algorithm, we state and prove the following claims:

1. There exists a pair of polynomials $$(W,E)$$ of appropriate degrees such that $$W/E = f$$, the polynomial we want to recover.<br/><br/>*Proof*. Let $$E(x) = \prod_{i : y_i \neq f(\alpha_i)} (x-\alpha_i)$$, i.e., $$E(\alpha_i)$$ is zero iff an error was made when transmitting the $$i$$-th symbol, and let $$W(x) = E(x)f(x)$$.[^eloc] Then we claim that for all $$x \in \mathbb{F}_q$$, $$E(x)y_i = W(x)$$. This follows since if $$y_i = f(\alpha_i)$$, then $$E(\alpha_i)f_i = E(\alpha_i) f(\alpha_i) = W(\alpha_i)$$, while if $$y_i \neq f(\alpha_i)$$, $$E(\alpha_i) = W(\alpha_i) = 0$$. Furthermore, by our assumption, $$\text{deg}(E) \leq t$$, since $$\Delta(y_i,(f(\alpha_1),\ldots,f(\alpha_q))) \leq t$$, while $$\text{deg}(W) = \text{deg}(E) + \text{deg}(f) < t+k$$. $$\blacksquare$$
2. The first step can be implemented *efficiently*. This follows since finding such $$(W,E)$$ is equivalent to solving a system of linear equations in the coefficients of $$W$$ and $$E$$; Gaussian elimination therefore can be used to find such coefficients.
3. If another pair of polynomials $$(U,F)$$ satisfies the constraints of the algorithm, then $$UE=WF$$. Note that this implies that $$F$$ divides $$U$$ and that $$F/U = W/E$$.<br/><br/>*Proof*. Note that $$\text{deg}(UE) \leq \text{deg}(U) + \text{deg}(E) < k+2t$$; this also applies to $$WF$$. Then the polynomial $$R(x) = U(x)E(x)-W(x)F(x)$$, if nonzero, is a polynomial of degree strictly less than $$k+2t < k+(n-k+1) = n+1$$, i.e., $$\text{deg}(R) < n$$. But $$R(x)$$ vanishes *everywhere* on $$\mathbb{F}_q$$, so we may conclude that is in fact the zero polynomial, and $$UE = WF$$. $$\blacksquare$$

Together with the fact that polynomial long division can also be done efficiently, we conclude that this is an efficient algorithm that always correctly recovers $$f$$, given that it exists.

### List-decoding

A natural generalization of the decoding problem for error-correcting codes is the problem of *list-decoding*. Say we want to correct $$p$$ errors, where $$p \geq d/2$$. Unique decoding is no longer possible, but it might still be helpful to return a short list of all possible decodings. Formally, a code $$\mathcal{C}$$ is $$(p,L)$$-list-decodable iff for all $$w \in \Sigma^n$$, $$\vert\text{Ball}(w,p) \cap \mathcal{C}\vert \leq L$$; that is, no potential error-filled string $$w$$ is within distance $$p$$ of more than $$L$$ codewords in the code $$\mathcal{C}$$. Again, we can state list-decoding as an algorithmic problem:

{% capture rs_list_problem %}
- *Parameters*: Output length $$n$$, input length $$k$$, and number of allowed errors $$p$$.
- *Input*: A sequence $$\vec{y} \in \mathbb{F}_q^n$$.
- *Output*: All polynomials of degree less than $$k$$ such that $$\Delta(\vec{y},(f(\alpha_1),\ldots,f(\alpha_q))) \leq p$$.
{% endcapture %}
{% include box.html content=rs_list_problem title="Problem (Reed-Solomon list-decoding)" %}

There are a few questions off the bat --- How large can $$p$$ be? Why is the number of such polynomials even polynomially bounded in $$n$$ (else no efficient algorithm could output them)? The theoretical limit for polynomially-bounded list sizes is something like $$p \leq (1-\sqrt{R})n$$, where $$R$$ is the rate of the code. We will present a relatively simple way to list-decode up to distance $$(1-2\sqrt{R})n$$ (compare to the unique-decoding limit of distance roughly $$(1-R)n$$). We will denote by $$\mathbb{F}_q[x_1,\ldots,x_n]$$ polynomials in the variables $$x_1,\ldots,x_n$$ and coefficients in $$\mathbb{F}_q$$. For a variable $$x_i$$, we will let the *$$x_i$$-degree* of $$f\in\mathbb{F}_q[x_1,\ldots,x_n]$$ be the degree of $$f$$ when we treat $$f$$ as a univariate polynomial by counting all $$x_j$$ for $$j \neq i$$ as constants.

{% capture rs_list_algorithm %}
1. Find a polynomial $$Q \in \mathbb{F}_q[x,y]$$ with $$\text{deg}_X(Q) \leq L$$ and $$\text{deg}_Y(Q) \leq n/L$$ such that for all $$i \in \{1,\ldots,n\}$$, $$Q(\alpha_i, y_i) = 0$$.
2. Factor $$Q$$. For each factor in the form $$y - f(x)$$:
    1. If $$\text{deg}(f) < k$$ and $$\Delta(\vec{y},(f(\alpha_1),\ldots,f(\alpha_q))) \leq p$$, output $$f$$.
{% endcapture %}
{% include box.html content=rs_list_algorithm title="Algorithm (Reed-Solomon list-decoding)" %}

It is a nontrivial but well-known fact that polynomials over finite fields can be efficiently factored. The correctness of this algorithm follows from the following claims:

1. There exists such a polynomial $$Q$$, and it can be done efficiently. This follows linear-algebraically: Finding $$Q$$ is equivalent to solving a linear system with $$n$$ constraints (the evaluations of $$Q$$ at the pairs $$(\alpha_i,y_i)$$) and $$(L+1)(n/L+1) = n+L+n/L+1 > n$$ unknowns. These constraints are homogeneous, so a solution exists; it can be efficiently found (as in the Welch-Berlekamp algorithm) by Gaussian elimination.
2. If there is a polynomial $$f \in \mathbb{F}_q^{<k}$$ such that $$\Delta(\vec{y},(f(\alpha_1),\ldots,f(\alpha_q))) \leq p$$, and $$Q$$ satisfies the above constraints, then $$y - f(x)$$ will divide $$Q$$.<br/><br/>*Proof*. Define $$R(x) = Q(x,f(x))$$. $$y-f(x)$$ divides $$Q$$ iff $$R$$ is the zero polynomial. But if $$R$$ is nonzero, $$\text{deg}(R) \leq \text{deg}_x(Q) + \text{deg}(f) \cdot \text{deg}_y(Q) \leq L + (\frac{n}L) (k-1)$$. And at the same time, for $$n-p$$ values of $$i$$, $$R(\alpha_i) = Q(\alpha_i,f(\alpha_i)) = Q(\alpha_i,y_i) = 0$$, and so $$\text{deg}(R) \geq n-p$$. So we have a contradiction if $$n-p > L + (\frac{n}L) (k-1)$$, and we can conclude that $$R$$ is zero. $$\blacksquare$$

Fixing $$L = \sqrt{n(k-1)}$$ yields $$n-p > 2\sqrt{n(k-1)}$$, i.e., $$p < n-2n\sqrt{(k-1)/n}$$. So as $$n$$ grows, we can correct arbitrarily close to $$(1-2\sqrt{R})n$$ errors.

### Further questions
There are of course many directions that one could go in to attempt to further improve or generalize these codes; I'll briefly mention three:

1. One major issue with the Reed-Solomon codes as stated is that the alphabet size $$q$$ must scale with the length of the messages we transmit; unfortunately, in the real world, we can only transmit $$1024$$-bit messages in the binary alphabet, not over $$\mathbb{F}_{1024}$$! And if we translated the alphabet $$\Sigma$$ into binary directly, the distance of our code would decrease by a factor of $$\log_2 \vert\Sigma\vert$$, where $$\Sigma$$ is the alphabet). A better idea is to *concatenate* the Reed-Solomon code with a good code over the binary alphabet: First encode the message in blocks using this small-alphabet code, and then encode the blocks using the Reed-Solomon code.
2. The Reed-Solomon codes can be generalized to *Reed-Muller codes*, where we interpret the message as coefficients of a multivariate polynomial, not a univariate polynomial. Depending on the specific choices for the number of variables, message lengths, etc., instances of Reed-Muller codes include not just Reed-Solomon codes but other useful families of codes like Hadamard and BCH codes.
3. Reed-Solomon codes can be made more efficient by, instead of recording the evaluations of a polynomial on an entire field, picking a strategic "less redundant" subset. This allows us to increase the rate of the code. Examples of such codes those of [Goppa] and [Garcia-Stichtenoth].

### References

The relevant original papers are (citations from Wikipedia):

* Reed, Irving S.; Solomon, Gustave (1960), "Polynomial Codes over Certain Finite Fields", Journal of the Society for Industrial and Applied Mathematics, 8 (2): 300–304.
* US 4,633,470, Welch, Lloyd R. & Elwyn R. Berlekamp, "Error Correction for Algebraic Block Codes", published September 27, 1983, issued December 30, 1986.

The textbook is:

* Guruswami, Venkatesan; Rudra, Atri; and Sudan, Madhu, *Essential Coding Theory*, 2019 (work in progress).

 Thanks also to Jyotsna Rao for editing this post.

<br/>
<hr/>

[^fields]: A *finite field* is a finite set where there are multiplication and addition operations with the usual properties (in particular, nonzero elements have multiplicative inverses). If you're not familiar with finite fields, just restrict to the case where $$q$$ is a *prime* (not just a prime power); then $$\mathbb{F}_q$$ is just the integers modulo $$q$$; you'll lose little generality. (It is a standard theorem of algebra that there only exist finite fields of prime power order, and these fields are unique up to isomorphism. See more information on [Wikipedia](https://en.wikipedia.org/wiki/Finite_field).)
[^mantra]: This statement does not follow from the fundamental theorem of algebra; it is trickier in the case of finite fields! Note that in $$\mathbb{F}_q$$ for prime $$q$$, the polynomial $$x^q-x$$ vanishes everywhere by Fermat's little theorem. But it is true (Proposition 5.2.3 in [Sudan-Guruswami-Rudra]) that in any field field $$\mathbb{F}_q$$, all nonzero polynomials of degree less than $$t$$ have fewer than $$t$$ roots. They call this the "degree mantra"; its proof is straightforward.
[^eloc]: $$E(x)$$ is called an *error-locating polynomial* for the received sequence $$\vec{y}$$, and $$(E,W)$$ together make an *error-locating pair*.