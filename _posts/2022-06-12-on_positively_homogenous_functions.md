---
layout: post
title: On positively homogenous functions
---

So, say we have a function $f : \mathcal{X} \to \mathcal{Y}$, where $\mathcal{X}$ and $\mathcal{Y}$ are both real vector spaces. We say $f$ is **positively homogeneous of degree $k$** if for any scalar $\alpha > 0$ and $x \in \mathcal{X}$, we have that $f(\alpha x) = \alpha^k f(x)$. Here $k$ is usually a positive integer.

Note that this implies that $f(\vartheta_\mathcal{X}) = \vartheta_{\mathcal{Y}}$ (where $\vartheta$ refers to the zero vectors in the respective vector spaces). We can note that $\vartheta_{\mathcal{X}} = 2 \vartheta_{\mathcal{X}}$ so $f(\vartheta_\mathcal{X}) = f(2 \vartheta_{\mathcal{X}}) = 2^k f(\vartheta_{\mathcal{X}})$.

Okay, so that's the formal definition. What's an intuition for this? Well, we can think of a positively homogeneous function as a function that acts on *directions* rather than vectors. Put another way, a positively homogeneous function is defined entirely by two things: its degree $k$ and its values on the unit circle. 

Formally, this means that for any argument $x$, we can let $v = x / \|x\|$ be the unit vector in the direction of $x$, and $\alpha = \|x\|$ be the magnitude of $x$. Then, $f(x) = f(\alpha v) = \alpha^k f(v)$. Thus, if we know the values of $f(\cdot)$ for all unit vectors $v$, then we know the value of $f(x)$ for all $x$. I've drawn this out below.

![Visualization of the projection onto the unit sphere.](/assets/images/unit_circle_proj.png)

Very concretely, let's suppose the domain of $f$ is $\mathbb{R}^2$. Then, we can take $x = (x_1,x_2)$ and put it in polar coordinates, let $r = \sqrt{x_1^2 + x_2^2}$ be the magnitude and let $\theta = \tan^{-1}(x_2/x_1)$ be the angle. Then, there exists some function $g : \mathbb{R} \to \mathcal{Y}$ such that $f(x) = r^k g(\theta)$. $f(\cdot)$ can be separated into the part that acts on the magnitude $r$ and the part that acts on the angle $\theta$. 
Slightly more generally, for $\mathbb{R}^n$, we can think of putting the function in generalized spherical coordinates, and then the one dimension corresponding to the magnitude of the vector can be separated out as above.

In this sense, a positively homogeneous function can be thought of as the function losing one degree of freedom: the way the function varies as the magnitude of the input changes is set by the degree $k$.

So, a positively homogeneous function is essentially a function which acts on directions. Let's put this intuition to use and derive Euler's theorem. For simplicity, let's suppose the co-domain $\mathcal{Y} = \mathbb{R}$, so $f(\cdot)$ is a positively homogeneous functional.

Here's how I like to state Euler's theorem, which differs slightly from the texts I've seen. 
Recall the definition of the **directional derivative**, which I will denote $D_v f(x)$. This is interpreted as the derivative of the function $f$ at the point $x$ in the direction $v$. It's given by:

$$D_v f(x) = \lim_{h \downarrow 0} \frac{f(x + hv) - f(x)}{h}$$

For each direction $v$, we define the domain of $D_v f(\cdot)$ as the values of $x$ such that this limit exists.

One way to think about this direction derivative is as follows. Once we fix the direction $v$ and the point $x$, we define a function $g : \mathbb{R} \to \mathbb{R}$ as $g(h) = f(x + hv)$. If $x$ is in the domain of $D_v f(\cdot)$, then $g$ will be differentiable at $0$, and we simply let $D_v f(x) = g'(0)$. Put another way, we define a function that essentially takes a one-dimensional slice out of the domain of $f$, and then differentiate that function.

Okay, so Euler's theorem states that $D_x f(x) = k f(x)$. It's perhaps a surprising theorem at first blush: the left-hand side has statements about the derivative of $f$, and yet the right-hand side has no differentiation whatsoever. The secret sauce is in the fact that $x$ is used as both the point of differentiation **and** the direction here.

After all, if you start at a point $x$ and then move in the direction $x$ a little bit, you are simply increasing the magnitude of $x$ without changing the direction. As we specified before, positively homogeneous functions are very specific in how they vary when the magnitude is the only thing that changes. (It's easy to see the theorem for the case where $x = \vartheta$, the zero vector, so we're going to suppose that $x$ is non-zero throughout this discussion.)

Pushing forward in this intuition formally, note the following holds by positive homogeneity: 

$$f(x + hx) = f( (1+h) x) = (1+h)^k f(x)$$

In words: if we start from the point $x$ and move a magnitude of $h$ in the direction $x$, then it's the same as scaling $x$ by $(1+h)$. This nicely allows us to invoke positive homogeneity. Thus, looking at the directional derivative:

$$D_x f(x) = \lim_{h \downarrow 0} \frac{f(x + hx) - f(x)}{h} = \lim_{h \downarrow 0} \frac{(1+h)^k f(x) - f(x)}{h} = f(x) \lim_{h \downarrow 0} \frac{(1+h)^k - 1}{h}$$

Now, this limit on the right-hand side is simply the derivative of $g(h) = (1+h)^k$ evaluated at $h = 0$. Well, $g'(0) = k$. Thus: $D_x f(x) = k f(x)$.

The more typical way you'll see this theorem stated is as follows. If $f$ is positively homogeneous of degree $k$ and differentiable, then $\langle \nabla f(x), x \rangle = k f(x)$. Note that when the function $f$ is differentiable, we have that $D_v f(x) = \langle \nabla f(x), v \rangle$, so the two line up in the case where $f$ is differentiable. 

However, the way I phrased it above, we didn't need $f$ to be differentiable. $x$ will *always* be in the domain of $D_x f$, for the reasons I stated above: the behavior of positively homogeneous functions along magnitude changes is completely specified by the degree of positive homogeneity $k$.

Anyway, in summary, when we state a function is positively homogeneous of degree $k$, we're essentially specifying its behavior along one degree of freedom: the magnitude of the input argument. As such, when you see this property invoked in proofs (or are considering assumptions to add to your paper where the proof doesn't quite seem to go through), it should take advantage of the structure imposed by positive homogeneity somewhere. In particular, you should see the `magnitude' separated out in some meaningful way along the proof, and then that separation will likely be used to get the desired result. Positive homogeneity alone may not tell us what the function does along the unit circle, but it does tell us *exactly* what happens when we scale the input arguments.

A cool example of the application of these intuitions is in [Chizat and Bach's *On the Global Convergence of Gradient Descent for Over-Parameterized Models using Optimal Transport* (2018)](https://arxiv.org/abs/1805.09545). In this paper, you can see this idea repeatedly in Appendix C. They define an operator $h^2$, which eats in positive measures on $\mathbb{R}^d$, and spits out positive measures on $\mathbb{S}^{d-1}$, the unit sphere in $\mathbb{R}^d$. For a positive measure $\mu$ on $\mathbb{R}^d$, they define $h^2(\mu)$ as the measure satisfying:

$$\int_{\mathbb{S}^{d-1}} \varphi(\theta) dh^2(\mu)(\theta) = \int_{\mathbb{R}^d}|u|^2 \varphi(u/|u|) d\mu(u)$$

Note the following about the variables of integration: the $\theta$ argument on the left-hand side lives in the unit sphere, whereas the $u$ argument on the right-hand side lives in $\mathbb{R}^d$. Yet, in both cases, the function $\varphi$ is only evaluated on the unit sphere, since on the right-hand side it is normalized before being passed as an argument. 

What's the intuition for this? Well, let's take a positively homogeneous function $f$ of degree $2$. Again, the instinct here is that the $f$ essentially only acts on directions. By positive homogeneity, we have that:

$$f(u) = |u|^2 f(u/|u|)$$

So, if we take some measurable set $B \subseteq \mathbb{S}^{d-1}$, we can think of this as a set of directions we want to integrate across. We can also define:

$$\tilde B = \{ x : x / |x| \in B \} \subseteq \mathbb{R}^d$$

This is the set of all vectors in $\mathbb{R}^d$ pointing in a direction in $B$. The definition above gives us that:

$$\int_{B} f(\theta) dh^2(\mu)(\theta) = \int_{\tilde B} f(u) d \mu(u)$$

The measure $dh^2(\mu)$ lets us integrate $2$-positively homogeneous functions across $\mu$, so long as the set we're integrating across is a set of directions. 
Put another way, the operator $h^2$ essentially projects the measure on $\mathbb{R}^d$ onto $\mathbb{S}^{d-1}$, scaling things in a fashion that respects the positive homogeneity.

With this projection, the middle part of the proof now restricts the relevant functionals to the unit sphere to see how the 'direction' evolves across time, and the proof finishes with an analysis of how the 'radial component' (which I've been referring to as the magnitude in this post) evolves across time. The projection $h^2$ formally allows the authors to analyze the dynamics on the unit sphere and the dynamics of the magnitude separately. It is a very neat application of positive homogeneity!
