# CS148-Homework-5-Sampling-and-Geometry-solved

Download Here: [CS148 Homework 5: Sampling and Geometry solved](https://jarviscodinghub.com/assignment/homework-5-sampling-and-geometry-solution/)

For Custom/Original Work email jarviscodinghub@gmail.com/whatsapp +1(541)423-7793

You’ll notice that this problem set is a few more pages than the usual CS 148
homework; part of this problem set is a reading assignment. The problems are
intended to make sure you understand both what we’ve covered in class and
what the narration below discusses: You are responsible for both on the final
exam!
In the past few weeks, we have covered a diverse set of topics relevant to computer graphics,
from sampling and Fourier theory to computer aided geometric design. In this homework, we
will be exploring a number of these topics to help you get better acquainted with the issues we
have discussed in class.
We’ll start by discussing some of the details of sampling theory laid out in class to help determine the resolution you need to display different continuous images. Recall that we stated the
following “theorem” in class:
Theorem(-ish). Any function can be written as a combination of simple wiggles.
Of course, the word “any” here is very suspect, but as computer scientists we’ll ignore the
intricacies of Lebesgue integration and Schwartz distributions in favor of an entirely un-rigorous
approach.1
Before we define the Fourier transform, we should state a famous mathematical relationship
that you likely have seen before:
e
iθ = cos θ + i sin θ (1)
This equation often is called “Euler’s Formula.” Let’s fill in some details:
• e = 2.718 . . . is the natural logarithm base.
• i =
√
−1 is the imaginary unit of the complex plane C.
• θ ∈ R is any real number.
If you never have seen (1), you should make the following straightforward observation: This equation makes no sense. And, you’re not wrong! In particular, raising any number to an imaginary
exponent i isn’t a reasonable operation in the usual sense of exponentiation as “repeated multiplication.”
1Please come to Justin’s office hours or post on Piazza if you would like work out the details of making this theory
more rigorous. Some fascinating and deep mathematics are hiding in the straightforward-looking derivations we cover
in CS 148!
1
In fact, in many ways we can think of Euler’s formula as a notational convenience. We can prove
that the right hand side of (1) behaves identically to exponentiation in almost every possible way.
This observation allows us to compactify derivations of many facts we know from high school
trigonometry. For instance, consider the following derivation:
cos(θ + φ) + i sin(θ + φ) = e
i(θ+φ) by (1)
= e
iθ
e
iφ by properties of exponentiation
= (cos θ + i sin θ)(cos φ + i sin φ) by (1)
= (cos θ cos φ − sin θ sin φ) + i(sin θ cos φ + cos θ sin φ) since i
2 = −1
Make sure you understand each step here before moving on!
But, what did we just show? If you take the real and imaginary components of the left and
right hand sides of the derivation above separately, we find:
cos(θ + φ) = cos θ cos φ − sin θ sin φ
sin(θ + φ) = sin θ cos φ + cos θ sin φ
You probably worked much harder to prove these statements in high school trigonometry.
Anyway, our goal today is to understand the Fourier transform of a function. We now have all
the tools we need to do so.
Definition (Fourier Transform). The Fourier transform of a function f : R → R is the function ˆ
f(ξ)
given by
ˆ
f(ξ) = Z ∞
−∞
f(x)e
−2πixξ
dx (2)
The variable ξ here represents a frequency. So, ˆ
f(ξ) represents the “component” of f that
wiggles at frequency ξ.
Problem 1 (10 points). Recall that in Lecture 11 of CS 148 we stated that the Fourier transform does the
“simplest possible thing:” multiplying a function against a wiggle at a fixed frequency and integrating. Use
Euler’s formula (1) to justify why the Fourier transform (2) does exactly this. Why does ˆ
f(ξ) need real and
imaginary components?
As tempting as it is for your mathematician instructor, we will not derive most of the (beautiful) relationships between properties of a function and properties of its Fourier transform. There
is, however, one relationship that is fundamental to the sampling theory we discussed in lecture.
Problem 2 (15 points). Take any real number a > 0, and define h(x) = f(ax). Derive the following
relationship:
ˆh(ξ) = 1
a
ˆ
f

ξ
a

(3)
Explain how this relationship substantiates the claim made in class that increasing the rate at which you
sample a (band-limited) function makes it less likely that you will see artifacts.2
2For students with a strong math background, note that in CS 148 you need not be concerned with whether your
integrals converge or are well-defined: feel free to apply and reasonable-looking operation without regard for such
analytical details!
2
Figure 1: For problem 3(a).
Hint: To derive (3), substitute h into the definition of the Fourier transform and make the substitution
y = ax.
There are myriad other facts we could derive from the Fourier transform ˆ
f that are relevant to
sampling theory as it applies to computer graphics, but we’ll abandon our discussion at this point
in favor of moving to the topic of geometric modeling.
Problem 3 (10 points). (a) The control points of a quadratic B´ezier curve g(t) and a cubic B´ezier curve
f(t) are shown in Figure 1. Construct the points g(3/2) and f(1/3). You’ll need to turn in a copy of
Figure 1 with your constructions drawn on top; you may wish to enlarge these structures and/or print
them on separate pages for more space. (b) Find the (quadratic and cubic, resp.) blossoms of the functions
g(t) = t
2 − 2t + 1 and h(t) = (t − 2)
3
.
One of the key ideas of computer-aided geometric design (CAGD) as it pertains to curves is
that of finding a basis for polynomial functions of a given degree. As we discussed in lecture, the
idea of a basis here is slightly more abstract than what you might have seen in Math 51, so it’s
worth putting some thought into our construction.
We consider a basis of the set of polynomials of degree n to be a set of n + 1 polynomial
functions p1(t), . . . , pn+1(t) such that any degree-n polynomial can be written as a linear combination of these pi
’s. For example, an obvious basis for the degree-three polynomials would be
p1(t) = 1, p2(t) = t, p3(t) = t
2
, p4(t) = t
3
. Why? Because the general form of a degree-three
polynomial is at3 + bt2 + ct + d, or equivalently ap4(t) + bp3(t) + cp2(t) + dp1(t).
Certain polynomial bases are convenient for certain problems, so a strategy in CAGD is to
work in a basis that simplifies our math as much as possible. We explored this strategy in class
when we derived the Hermite basis, which simplified the problem of finding a curve with given
begin and end points/tangents. In our final written problem, we will derive an alternative basis
for cubic polynomials simplifying math for Bezier curves. ´
Problem 4 (15 points). Suppose we label the control points~a,~b, ~c, and d of a cubic curve in Figure 2 and ~
use the structure drawn to find the point f(t) (assume the control points specify the curve between f(0)
and f(1)). Label the constructed points as linear combinations of the control points; we provide you with
one label to get you started. Use your label for f(t) to define the Bernstein basis for cubic polynomials, that
is, a basis that makes it easy to write down the cubic curve associated with a set of four control points.
3
Figure 2: For problem 4.
Figure 3: Examples of MLS output.
For the coding part of this assignment, you will implement the Moving Least Squares (MLS)
image deformation algorithm introduced in SIGGRAPH 2006.3 Examples of the output of MLS
are shown in Figure 3. The purpose of this algorithm is fairly straightforward: The user marks
a number of “handles” on an image and then starts moving them around. As the handles are
moved, the image deforms smoothly while satisfying the constraints that the handles are mapped
to their targets. MLS can be used to achieve lots of interesting image effects with relatively simple
computations.
To motivate MLS, we first consider a slightly easier problem. Let’s say we mark a number of
points ~p1, . . . ,~pn ∈ R2 on the plane, and we specify a list of targets ~q1, . . . ,~qn ∈ R2
. We wish to
find an affine transformation of the plane given by ~p 7→ M~p +~t for some M ∈ R2×2
,~t ∈ R2
such
that M~pi +~t ≈ ~qi
for each i ∈ {1, . . . , n}. When is n > 2, the ≈ is key: it might be the case that no
affine transformation can map all the ~pi
’s to their corresponding ~qi
’s exactly!
Thus, we can only hope to approximate such a relationship. To this end, we’ll introduce one
3You’re encouraged to read the original paper for a more detailed discussion. Note that the paper uses row rather
than column vectors, so their math is a bit different.
4
more set of inputs: a set of “weight” values w1, . . . , wn > 0. A large weight wi says we really care
that ~pi maps to ~qi
, while a small wi  1 means we don’t really care if M and~t don’t do a good job
mapping ~pi
to ~qi
.
Note that if M~pi +~t ≈ ~qi
then M~pi +~t −~qi ≈ ~0. In other words, we desire that kM~pi +~t −
~qik
2 ≈ 0. So, let’s define an energy:
E(M,~t) =
n
∑
i=1
wikM~pi +~t −~qik
2
(4)
We can make a number of important observations about E:
• We always have E ≥ 0.
• If there exist ~t and M such that ~qi = M~pi +~t exactly for all i ∈ {1, . . . , n}, then E will be
minimized with value 0 at this point.
• When such a zero minimum is not possible, the minimum E > 0 occurs when M and ~t
give the best affine map approximating ~pi
7→ ~qi
in a “least squares” sense. The weights wi
prioritize with (~pi
,~qi) pairs matter the most.
Thus, if the user inputs lots of pairs (~pi
,~qi), we can frame an optimization problem to find M and
~t as follows:
min
M∈R2×2
,~t∈R2
E(M,~t) (5)
You probably spent much of calculus class solving problems exactly of this nature! Simply take
derivatives of E with respect to the elements of M and~t, set them to zero, and solve.
We’ll resist the urge to force you to derive these formulas yourself, although you’re encouraged
to check them on scratch paper; our discussion above plus a few tricks from Math 51 are all you
need. Instead, we’ll jump right to the solution of our minimization problem (5). To clean up our
notation a bit, let’s define some helper variables:
~p
∗ =
∑
n
i=1 wi~pi
∑
n
i=1 wi
(6)
~q
∗ =
∑
n
i=1 wi~qi
∑
n
i=1 wi
(7)
It’s easy to differentiate (5) with respect to the elements of~t (at least try this part at home!), yielding
the following relationship when we set this derivative to zero:
~topt = ~q
∗ − Mopt~p
∗
(8)
That is, we can find the optimal translation~topt easily enough once we know the optimal matrix
Mopt.
Finding Mopt takes a bit more bookkeeping. We’ll need two more sets of helper variables:
pˆi = ~pi −~p
∗
(9)
qˆi = ~qi −~q
∗
(10)
5
We can reduce finding Mopt to a least-squares problem, so when the smoke clears we’ll get the
following “normal equation” solution:
Mopt =
n
∑
j=1
wjqˆjpˆ
>
j
! n
∑
i=1
wi pˆi pˆ
>
i
!−1
(11)
This finishes our story. From the inputs (~p1,~q1, w1), . . . ,(~pn,~qn, wn) we can compute ~p
∗ and ~q
∗
.
We can use these to compute pˆi and qˆi
for all i. Then, we use (11) to compute Mopt. Finally, we
find~topt using (8). The formulas might look complicated, but they’re quite simple to evaluate; the
2 × 2 inverse in (11) can be found in closed-form with the usual formula (built into Eigen using
the .inverse() method of Matrix2d).
We may wish to put additional constraints on Mopt. It’s easy to see that regardless of our
constraints on Mopt, the formula (8) for ~topt stays the same. This aside, if we want only to consider similarity matrices M that contain no shear–that is, they only can rotate and scale–then we
constrain M>M = λ
2
I for some λ ∈ R (think about why!) and find:
M
similarity
opt =
1
µ
n
∑
i=1
wi

qˆ
>
i
(−qˆ
⊥
i
)
>


pˆi −pˆ
⊥
i

(12)
where
µ =
n
∑
i=1
wikpˆik
2
(13)
If we force M only to encode rotations without any scaling, then (12) still works, but we replace µ
with
µ˜ =
vuut

n
∑
i=1
wi(qˆi
· pˆi)
!2
+

n
∑
i=1
wi(qˆi
· pˆ
⊥
i
)
!2
(14)
Here, for vector~a = (a1, a2) we denote~a
⊥ = (−a2, a1).
MLS simply applies the formulas we developed above with a clever choice of the wi values.
We’re going to render an image by drawing a k × k grid of quads with evenly-spaced texture
coordinates. In our code the grid of texture coordinates is stored in the variable textureCoords;
you should not change the values in this array. We’ll deform the grid to a new set of positions
(stored in imageCoords) using the MLS algorithm and render the deformed image using textured
triangles; see display() to see our basic setup.
The user shift-clicks the control points ~pi
to make red handles appear (shift-clicking those red
handles again makes them disappear); the indices of these points in imageCoords are stored in the
set active. The user then can drag the handles to new targets ~qi
, the positions of which are stored
in imageCoords. This much functionality is implemented for you in the skeleton code.
Your job is to implement deformImage(), which writes new values for elements of the array
imageCoords. The basic algorithm goes like this:
• Iterate over each texture coordinate ~p in the array textureCoords.

• If ~p is one of the ~pi
’s, then its position in imageCoords is ~qi and can be left alone. Otherwise
proceed with the steps below.
• Compute weights wi = k~pi − ~pk
−2α
for the provided constant α > 0. Recall that ~pi denotes
the texture coordinate of the ith point in active. Notice what this choice of wi
is doing:
Control points that are close to ~p get more weight than those that are far away.
• Compute Mopt and~topt using the weights wi you just computed and the formulas above.
• Replace the position in imageCoords with ~q = Mopt~p +~topt.
In other words, each (sampled) point on the base texture computes its own least-squares map and
uses that map to find a target.
Problem 5 (50 points). Implement MLS deformation starting from the skeleton code. You must implement
the affine, similarity, and rotation-only versions of the algorithm, using command line options stored in
deformationType to determine what to do in the application.
Problem 6 (5 points extra credit). When does our choice of wi
in MLS break down? Can you suggest
a replacement? Describe your solution in the written homework; no need to add it to your code, as the
implementation change might (hint!) require a using a structure other than a grid mesh–a considerable
change!
