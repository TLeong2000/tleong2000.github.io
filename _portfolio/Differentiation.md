---
title: "Differentiation beyond Single-Variable Functions"
excerpt: ""
collection: portfolio
---

## Preamble

Let \\(f : X \rightarrow Y \\) be a function whose domain is (some subset of) a vector space (e.g. \\(\mathbb{R}^n \\)). If we try to define the derivative of such a function the same way we define the derivative of a scalar-domained function:

$$\forall x \in X : f'(x) = \lim_{h \to 0} \frac{f(x+h)-f(x)}{h} $$

$$\Leftrightarrow (\forall \epsilon > 0)(\forall \delta > 0) : 0 < |h| < \delta \Rightarrow \left|\frac{f(x+h)-f(x)}{h}-f'(x) \right|<\epsilon $$

...we immediately run into issues.

First, because the domain is vector-valued, that means that \\(h \\) must also be vector-valued as well. However, because it is impossible to define a multiplication operation for an arbitrary vector space that is isomorphic to multiplication of real numbers, it is also impossible to define a division operation for an arbitrary vector space that is isomorphic to division of real numbers. We need to come up with a concept of derivative that does not involve dividing two vectors.

There is one concept that we can exploit to form a sensible definition of derivative that works regardless of whatever vector space the domain or codomain of \\(f \\) happens to be: a norm.

Notice that the absolute value in the consequent in the \\(ϵ-δ \\) definition of the derivative of a single-variable function can be re-written as a quotient of two absolute values:

$$ \left|\frac{f(x+h) - f(x)}{h} - f'(x)\right|= \left|\frac{f(x+h) - f(x) - f'(x)\ast h}{h}\right| = \frac{\left|f(x+h) - f(x) - f'(x) \ast h \right|}{\left|h \right|} $$

...for the rest of this document, I will denote this quotient as the <mark>remainder quotient</mark>.

The remainder quotient formulation is important, because the absolute value is a norm for the field \\(\mathbb{R}\\), and the codomain of any norm is always a scalar - subsequently, the quotient of two norms will always be a well-defined quantity.

However, we aren't done yet: notice that the numerator of our new consequent contains a \\(f'(x) * h\\) term. As mentioned earlier, it is impossible to define a multiplication operation for an arbitrary vector space that is isomorphic to multiplication of real numbers. So how do we proceed from here?

First, notice that for single-variable functions, the image of \\(x \in X \\) under \\(f' \\), aka \\(f'(x) \\), is a scalar. Given any scalar, multiplication of that scalar by another scalar is a linear transformation \\(\mathbb{R} \rightarrow \mathbb{R} \\), and because \\(h \in X \subseteq \mathbb{R} \\), we can say that \\(f'(x) \\) linearly transforms \\(h \\). The concept of linear transformation is what we will need to generalize differentiation and is what will allow us to extend the concept of tangent lines to tangent spaces.

Let \\(f \\) be a function from a Banach space \\(X \\) to another Banach space \\(Y \\). \\(\forall x,h \in X :\\) if \\($f(x+h)\\) and \\(f(x)\\) are defined, then \\(f(x+h) \in Y \wedge f(x) \in Y \\), and therefore \\(f(x+h)-f(x) \\) is a well-defined object that resides in \\(Y \\). If we want \\(f(x+h) - f(x) - \left(f'(x) \right)(h) \\) to be a well-defined object, then \\(f'(x) \\) needs to be a linear transformation \\(X \rightarrow Y \\).


## Fréchet Derivatives

We can finally synthesize a definition of differentiation for multivariable functions:

Let \\(f \\) be a function \\(V \subseteq X \rightarrow Y \\), where \\(X \\) and \\(Y \\) are Banach spaces. For any \\(a \in V \\) we define \\(f \\) to be \\(\colorbox{yellow}{Fréchet-differentiable at \\(a \\)} \\) if and only if there exists a bounded linear transformation \\(T_{a}f : X \rightarrow Y \\) such that the remainder quotient converges to \\(0 \\) as the displacement \\(h \\) goes to \\(0 \\):

$$\lim_{\left\Vert h \right\Vert \to 0} \frac{\left\Vert f(a+h) - f(a) - T_{a}f(h) \right\Vert}{\left\Vert h \right\Vert} = 0$$

$$\Leftrightarrow (\forall \epsilon > 0)(\exists \delta > 0)(\forall h \in X) : 0 < \Vert h \Vert < \delta \Rightarrow \Vert f(a+h) - f(a) - T_af(h) \Vert < \epsilon \Vert h \Vert $$

If such a linear transformation exists, we designate it the \\(\colorbox{yellow}{Fréchet derivative of \\(f \\) at \\(a \\)} \\). It is sometimes designated as the total derivative. Within physics and engineering contexts, the Fréchet derivative may also be referred to as the gradient, although within mathematical contexts, the word gradient is restricted to the dual vectors of the Fréchet derivatives of functions \\(\mathbb{R}^n \rightarrow \mathbb{R}\\). For functions \\(\mathbb{R}^n \rightarrow \mathbb{R}^m \\), the Fréchet derivative may be referred to as the Jacobian.

### Uniqueness

If the Fréchet derivative of a function at a point exists, it is unique. However, the proof for functions between arbitrary Banach spaces is less obvious than one would suspect.

Suppose that \\(L_1 \\) and \\(L_2 \\) are bounded linear transformations \\(X \rightarrow Y \\) but are not the same operator (\\(L_1 \neq L_2 \\)). By definition, this means:

$$\exists h \in X : L_1(h) \neq L_2(h) $$

$$\Leftrightarrow \exists h \in X : L_1(h) - L_2(h) \neq \mathbf{0}$$

Because a sum of linear operators is also a linear operator, and the preimage of any non-zero vector, under a linear operator, must be a non-zero vector, this statement is logically equivalent to:

$$\Leftrightarrow \exists h \in X : 0 < \Vert h \Vert \wedge \frac{\Vert (L_1 - L_2)(h) \Vert}{\Vert h \Vert} > 0$$

Because the image of a non-zero vector, under a linear operator, is a non-zero vector, the image of any non-zero scalar multiple of a non-zero vector, under a linear operator, is also a non-zero vector. This implies that the above statement is logically equivalent to:

$$\Leftrightarrow (\forall \delta > 0)(\exists h \in X) : 0 < \Vert h \Vert < \delta \wedge \frac{\Vert (L_1 - L_2)(h) \Vert}{\Vert h \Vert} > 0$$

$$\Leftrightarrow (\exists \epsilon > 0)(\forall \delta > 0)(\exists h \in X) : 0 < \Vert h \Vert < \delta \wedge \frac{\Vert (L_1 - L_2)(h) \Vert}{\Vert h \Vert} >= \epsilon$$

As per Triangle Inequality, the second proposition in the conjunction is logically equivalent to:

$$\Vert f(a+h) - f(a) - L_1(h) \Vert + \Vert f(a+h) - f(a) - L_2(h) \Vert >= \Vert (L_1 - L_2)(h) \Vert >= \epsilon \Vert h \Vert$$

...which through the Law of the Excluded Middle, is equivalent to:

$$\neg (\Vert f(a+h) - f(a) - L_1(h) \Vert + \Vert f(a+h) - f(a) - L_2(h) \Vert < \epsilon \Vert h \Vert)$$

Because \\(a < \frac{c}{2} \wedge b < \frac{c}{2} \Rightarrow a + b < c\\), by contraposition, the above statement implies:

$$\Rightarrow \neg (\Vert f(a+h) - f(a) - L_1(h) \Vert < \frac{\epsilon}{2} \Vert h \Vert \wedge \Vert f(a+h) - f(a) - L_2(h) \Vert < \frac{\epsilon}{2} \Vert h \Vert)$$

We plug this back in to an earlier statement to arrive at a negation of a conjunction of two statements:

$$\Leftrightarrow \neg \left((\forall \epsilon > 0)(\exists \delta > 0)(\forall h \in X) :\left(0 < \Vert h \Vert < \delta \Rightarrow \Vert f(a+h) - f(a) - L_1(h) \Vert < \frac{\epsilon}{2} \Vert h \Vert \right) \wedge \left(0 < \Vert h \Vert < \delta \Rightarrow \Vert f(a+h) - f(a) - L_2(h) \Vert < \frac{\epsilon}{2} \Vert h \Vert \right) \right)$$

This proves that if \\(L_1 \neq L_2 \\), they cannot both be Fréchet derivatives of the same function at the same point, and by contraposition, if two linear transformations are both Fréchet derivatives of the same function at the same point, they must be the same transformation. \\(\blacksquare \\)

> [!NOTE]
> As of the time I wrote this, I had yet to see anyone present a completely rigorous proof of this theorem - every "proof" I had seen of this theorem jumps from \\(\lim_{\Vert h \Vert \to 0} \frac{\Vert (L_1-L_2)(h) \Vert}{\Vert h \Vert} = 0 \\) to \\(L_1 = L_2 \\) without explaining anything in-between.

### Continuity of Differentiable Functions
For functions \\(\mathbb{R} \rightarrow \mathbb{R} \\), you are already aware that differentiability implies continuity. Does this still hold for functions on arbitrary Banach spaces?

We start with the definition of Fréchet differentiability:

$$(\forall \epsilon > 0)(\exists \delta > 0)(\forall h \in X) : 0 < \Vert h \Vert < \delta \Rightarrow \Vert f(a+h) - f(a) -T_af(h) \Vert < \epsilon \Vert h \Vert$$

Let us add \\(\Vert T_af(h) \Vert \\) to both sides of the consequent, and use Triangle Inequality to get:

$$\Leftrightarrow (\forall \epsilon > 0)(\exists \delta > 0)(\forall h \in X) : 0 < \Vert h \Vert < \delta \Rightarrow \Vert f(a+h) - f(a) \Vert < \epsilon \Vert h \Vert + \Vert T_af(h) \Vert$$

Because \(T_af\) must be a bounded linear operator, there must exist a non-negative real number \(C\) such that \(\forall h \in X : \Vert T_af(h) \Vert \leq  C \Vert h \Vert \). Therefore, the previous statement is equivalent to:

$$\Leftrightarrow (\forall \epsilon > 0)(\exists \delta > 0)(\forall h \in X) : 0 < \Vert h \Vert < \delta \Rightarrow \Vert f(a+h) - f(a) \Vert < \Vert h \Vert \left(\epsilon + C\right) $$

Note that whenever the antecedent is true, the consequent implies that \\(\Vert h \Vert \left(\epsilon + C\right) < \delta \left(\epsilon + C\right)$ \\).

Let us now define a new variable \\(\eta := \delta (\epsilon + C) \\). Note that \\(\delta > 0 \wedge \epsilon > 0 \Rightarrow \eta > 0 \\). Therefore, we conclude with:

$$\Rightarrow (\forall \eta > 0)(\exists \delta > 0)(\forall h \in X) : 0 < \Vert h \Vert < \delta \Rightarrow \Vert f(a+h)-f(a) \Vert < \eta$$

This proves that Fréchet differentiability of a function at a point implies continuity of that function at that point. \\(\blacksquare \\)

However, as with functions \\(\mathbb{R} \rightarrow \mathbb{R} \\), continuity at a point for functions between arbitrary Banach spaces is a necessary but insufficient condition for differentiability.

### Gateaux Derivatives

The definition of Fréchet derivative involves a vector \\(h\\) that represents a displacement in all directions at once.

However, what if we want to consider a displacement in each direction that occurs one direction at-a-time?

Let \\(f : V \subseteq X \rightarrow Y \\) be a function between arbitrary Banach spaces. We can describe a displacement along a certain direction as a scalar multiple \\(\tau \\) of the unit vector \\(\psi \\) corresponding to said direction.

\\(\forall a \in V : \\) We define \\(f \\) to be \\(\colorbox{yellow]{Gateaux-differentiable at \\(a \in V \\)} \\) if and only if there exists a bounded linear operator \\(\delta_af : X \rightarrow Y \\) such that \\(\forall \tau \psi \in X \\), the remainder quotient converges to \\(0 \\) as \\(\tau \psi \\) goes to \\(0 \\):

$$\lim_{\Vert \tau \psi \Vert \to 0} \frac{\Vert f(a + \tau \psi) - f(a) - \delta_af(\tau \psi) \Vert}{\Vert \tau \psi \Vert} = 0$$

$$\Leftrightarrow \left( \forall(\tau \psi) \in X \right)(\forall \epsilon > 0)(\exists \delta > 0) : 0 < \Vert \tau \psi \Vert < \delta \Rightarrow \Vert f(a + \tau \psi) - f(a) - \delta_af(\tau \psi) \Vert < \epsilon \Vert \tau \psi \Vert$$

Because we defined \\(\psi \\) to be a unit vector and \\(\tau \\) to be a scalar, this is equivalent to:

$$\Leftrightarrow \left( \forall(\tau \psi) \in X \right)(\forall \epsilon > 0)(\exists \delta > 0) : 0 < |\tau| < \delta \Rightarrow \frac{\Vert f(a + \tau \psi) - f(a) - \tau\delta_af(\psi) \Vert}{|\tau|} < \epsilon $$

$$\Leftrightarrow \left( \forall(\tau \psi) \in X \right)(\forall \epsilon > 0)(\exists \delta > 0) : 0 < |\tau| < \delta \Rightarrow \Vert \frac{f(a + \tau \psi) - f(a)}{\tau} - \delta_af(\psi) \Vert < \epsilon $$

Subsequently, an equivalent definition of Gateaux differentiability of \\(f \\) at \\(a \\) is the existence of a bounded linear operator \\(\delta_af : X \rightarrow Y \\) such that \\(\forall \psi \in X : \\) the image of \\(\psi \\) under \\(\delta_af \\) is equal to the limit of the difference quotient of \\(f \\) at \\(a \\) in the direction of \\(\psi \\):

$$\delta_af(\psi) = \lim_{\tau \to 0}\frac{f(a+\tau\psi) - f(a)}{\tau}$$

If such a linear operator \\(\delta_af \\) exists, we designate it as the \\(\colorbox{yellow}{Gateaux derivative of \\(f \\) at \\(a \\)} \\). The proof of uniqueness of the Fréchet derivative of a function at a point can easily be extended to prove uniqueness of the Gateaux derivative of a function at a point.



You may be wondering: "What does this have to do with Fréchet differentiation?"

Let \\(f \\) be Fréchet-differentiable at a point \\(a \in V \\). By definition of Fréchet differentiability, the following statement is true:

$$(\forall \epsilon > 0)(\exists \delta > 0)(\forall h \in X) : 0 < \Vert h \Vert < \delta \Rightarrow \Vert f(a+h) - f(a) - T_af(h) \Vert < \epsilon \Vert h \Vert$$

Now \\(\forall h \in X \\), we can re-write \\(h \\) as itself scalar multiplied by \\(1 \\), which is equal to itself scalar multiplied by its norm divided by its norm.

Let us define the variables \\(\tau := \Vert h \Vert \\) and \\(\psi := \frac{h}{\Vert h \Vert} \\). Obviously, \\(\frac{\Vert h \Vert}{\Vert h \Vert}h = \tau \psi \\). We can now re-write the statement of Fréchet differentiability as:

$$\Leftrightarrow (\forall \epsilon > 0)(\exists \delta > 0)(\forall \tau\psi \in X) : 0 < |\tau| < \delta \Rightarrow \Vert f(a+\tau\psi) - f(a) - T_af(\tau\psi) \Vert < \epsilon |\tau|$$

$$\Leftrightarrow (\forall \epsilon > 0)(\exists \delta > 0)(\forall \tau\psi \in X) : 0 < |\tau| < \delta \Rightarrow \Vert \frac{f(a+\tau\psi) - f(a)}{\tau} - T_af(\psi) \Vert < \epsilon $$

Note that the only logical difference between the above statement and the definition of Gateaux differentiability is the scope of the quantifiers: for the above statement, the quantifier \\(\left(\forall\tau\psi \in X \right)\\) is within the scope of the quantifier \\(\left(\exists \delta > 0 \right) \\), whereas in the definition of Gateaux differentiability, \\(\left(\exists \delta > 0 \right) \\) is within the scope of \\(\left(\forall\tau\psi \in X \right)\\).

Because \\(\exists x \forall y : \Phi (x,y) \Rightarrow \forall y \exists x : \Phi (x,y) \\), the above statement implies that \\(f \\) must be Gateaux-differentiable at \\(a \\). Since the Fréchet derivative is a bounded linear operator and satisfies this statement, if \\(f \\) is Fréchet-differentiable at \\(a \\), then the Gateaux derivative of \\(f \\) at \\(a \\) must be equal to the Fréchet derivative of \\(f \\) at \\(a \\). \\(\tombstone \\)
