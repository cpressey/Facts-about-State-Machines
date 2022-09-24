Facts about State Machines
==========================

Jump to: [Introduction](#introduction) | [Fundamentals](#fundamentals) | [Intermediate](#intermediate)
| [Statecharts](#statecharts) | [Implementation](#implementation) | [Advanced](#advanced)

## *Introduction*

### I hold the opinion that state machines are often misunderstood and under-applied

And that's why I wrote this.  The goal of this list of facts is not to teach
you what state machines are or how to use them; there are plenty of other resources for that.
Rather, the goal here is to motivate their usage and to highlight things about
them that are frequently overlooked, but nonetheless relevant.

If you are reading one of these facts and deem it trivial, or irrelevant, or
unsubstantiated, or, or, ... then I encourage you to just move on to the next one
in the hopes that you will find it more edifying.

## *Fundamentals*

### State machines are ubiquitous

They're all over the place.  Think of all the web apps, all the electronic devices,
all the household appliances, all the industrial machines that people interact with
every day.  For each one of them, we can formulate a state machine that describes
its reactive behaviour with a great degree of precision.

### A state machine is not a state machine diagram

A state machine is an abstract object -- a concept.  A state machine diagram
is a depiction of that abstract object.  Much like how the same number can be
equally well represented by a numeral (like "5") or a word (like "five"), the
same state machine can have multiple representations, different but equivalent.

### A state machine diagram is like a *map* of a system's reactive behaviour

It is like a map because, for a given state, you can see what transitions are
allowed into and out of that state.  You can see the paths by which the system
"travels" from one state to another, as well as seeing where there are no paths.

Just like a map, it doesn't have to (and probably shouldn't) contain every single
detail.  It needs only enough detail to allow you to orient yourself efficiently.

### A state machine is like a board game, and the diagram is like the board

You can imagine you have a counter, and it's sitting on one of the squares
(states) on the board.  You draw a card, and written on it is a word (an input).
Now, if there's an arrow going out from your square
that is labelled with that word, you slide your counter along it, moving
it to a new square.  But if there's no such arrow going out of your square,
your counter stays where it is.

### State machine diagrams can be read by non-technical stakeholders

Maps and board games are everyday things, so I hope the previous two metaphors
convince you that just about anyone, technically-minded or not, can grasp the
basic functioning of a state machine.

A non-technical stakeholder might still find a large diagram intimidating,
of course.  But by splitting a diagram into smaller diagrams,
or by reducing a diagram to a simpler diagram by leaving out details,
you can ease the reader into the structure of the reactive behaviour of the system.

### A state machine diagram allows reasoning about the system's reactive behaviour

If you are given a starting state and series of inputs, you can plot a
course through the state machine diagram and see what state you end up
in, and what actions occurred along the way.  By comparing this with your
intuition, or with reports of how the actual system actually behaves
(or specifications for how it _should_ actually behave), you can pinpoint where
changes need to be made.

### A state machine diagram allows reasoning about proposed modifications

Suppose we want to introduce a new operation into our system.  If we did,
what would happen in existing states when the events associated with that new
operation occur?  What _should_ happen?  Will new states need to be added
to capture what is going on with these events?  And how will those states
relate to existing states?

### State machines can be used for specification

A state machine diagram, presented prescriptively, establishes
the reactive behaviour that your system _should_ have.  The code itself can only
describe the behaviour that your system _does_ have.  The only way to
decide if the exhibited behaviour is correct, is to compare it to the
behaviour it _should_ have.  This is the idea of having a specification.

### State machines can be used to model user interfaces

Having heard somewhat uninformed statements like "I thought state machines
were only for physical devices" or "User interfaces aren't suitable for
modelling with state machines", which are plainly false, I feel I should
point this out.

In fact, there is an entire book about designing UIs using Statecharts,
[Constructing the User Interface with Statecharts (Horrocks, 1999)](https://archive.org/details/isbn_9780201342789)
(archive.org, borrowable online.)

It is noted in the book that using the Statecharts notation
([see below](#statecharts)) rather than a
flat state diagram will be helpful (virtually necessary) to address the
complexity found in most user interfaces.

### Most state machines are simple

A compiler, for example, has trivial reactive behaviour.  Diagramming
its state machine might not be the best use of your time.
But even simple state machines are sometimes worth working out as
diagrams, simply to confirm that they _are_ simple, and in exactly what way.

### A complex state machine means your system has complex behaviour

And anything interfacing with this system -- such as a human using it -- will face this
complexity, and the cost of this complexity.  This may prompt you to review the
behaviour.  Maybe the complexity is inherent... or maybe it can be simplified.

### Working out a state machine helps you understand your system's reactive behaviour

You won't get it right on the first try, and probably not the second or third try
either.  But each time you revise it, you'll learn something important about how
your system behaves.

### Studying a state machine can help you simplify the design of the system

To reduce the complexity of the system, you should eliminate complex things, like
concurrency and complex state interactions, where-ever you can.  Going through the state
machine diagram will help you understand where complex state interactions occur,
and may help you work out where they are actually needed, and where they could be
eliminated.

### Understanding a state machine will help you formulate useful tests

An arrow shows a transition that can happen when an input occurs.  What states can it
happen from?  We can look at the state machine diagram and answer that.  Now,
what about those _other_ states -- what should happen when the input occurs in those states?
What _does_ happen?  Test cases can be formulated to cover these possibilities.

## *Intermediate*

### State machines and finite automata are two different things

While similar in structure, the two are quite different in practice.

Finite automata (sometimes also called "finite state machines") are formally
defined abstractions in [automata theory](https://en.wikipedia.org/wiki/Automata_theory) (Wikipedia).
They are able to recognize some formal languages and not able to recognize
others, and they have practical applications in software, for example in
pattern matching in text documents.

A state machine, on the other hand, is a system design concept that originated
in [electrical engineering](https://en.wikipedia.org/wiki/Electrical_engineering) (Wikipedia.)  It relates the
states of a system by the possible transitions between them; those transitions are
triggered by inputs received from external sources.  The inputs are received at
(nominally) different times.  Making a transition, or arriving in or leaving a state,
may be guarded by a condition, and may trigger an action of some kind as a side-effect.
There is no pre-set constraint on the kinds of actions such a transition may trigger.

### The phrase "finite state" can be misleading and can be avoided

While a state machine typically does indeed have a finite and fixed number of _states_,
there is no set limit on the amount of _state_ that may be associated with the machine.
That state typically includes counters, timers, buffers, data stores, and so forth.

It might help to note that the word "states" is what's called in English a _count noun_
(like "pennies"), while the word "state" is a _mass noun_ (like "water").

Some terminology that has been proposed to make this distinction clearer includes
calling the finite set of states the "control state" and everything else the
"extended state".  Considering both of these together is sometimes called
"the state of the system".

The term "state machine" is now commonplace; you don't have to qualify it with
"finite".  System designers will usually understand what you mean when you say
"state machine".

### The "states" of the machine refer to the _modes_ of the system

There's a good argument to be made that the word "mode" would be a better
choice than the word "state" for referring to a member of the finite set of
control states.

If you ask yourself, "What modes can this system be in?", you'll likely
find that the answer coincides with the set of states of the state machine.

It's also consistent with the fact that this set is finite: it's
difficult to imagine a system with an infinite number of "modes".

But a terminology shift of this magnitude is unlikely to happen anytime
soon.  Everyone knows them as "state machines", and calling them
"mode machines" just wouldn't catch on.

### "States" are often qualitative while "state" is often quantitative

It's also been noted that the finite set of states tends to describe the
_qualitative_ state of the system, while the "extended" state tends to be
_quantitative_ in nature (counters and such).

### Being in exactly one state at any given time is helpful for reasoning

This quality of _mutual exclusion_ is very helpful when reasoning about
the behaviour of a state machine because, if the machine is in (for
example) the "waiting" state, you immediately also know that it is
_not_ in the "ready" state, and _not_ in the "rejected" state, and...
and so forth, for all other states.

### ...but the set of states need not be disjoint

Although it is very, very useful for reasoning about reactive behaviour
(see previous fact), it's not gospel.  The Statecharts paper (Harel, 1986)
([see below](#statecharts)) gives an
example of a diagram that shows two partially overlapping states
in Figure 41.

### A state machine diagram is not a flowchart

A flowchart is "self-propelled"; the transition that is followed out of a
decision point is determined solely by the decision made inside the decision point.
In a state machine, though, the triggers that cause the transitions are generally
_external_ to the system.  (It's _re_ active, remember.)

### ...but you can incorporate some flowchart elements in a state diagram

Sometimes it happens that an input causes a transition, but the ultimate
destination of that transition is not solely determined by the input; one
or more decisions have to be made in order to select the state to which
the machine will ultimately transition.  This can be captured with
multiple arrows between the same two states, with different conditions on
each arrow; or with "empty" states that don't represent states so much as
they represent decision points.  But there are valid objections
to both of these approaches -- the conditions can be complex, and the
"empty" states are artificial.  So there really is a case to be made that
decision points, like the diamond boxes from a flowchart, can be used in
a state machine diagram, when using them would make the behaviour clearer.
This should be recognized as being an advanced technique, however.

### A state machine does not specify the means by which the inputs are communicated

That is to say, there is no requirement that the inputs of the
state machine are messages sent directly to the state machine.

The state machine could be "listening for" and reacting to broadcast
events that other systems are reacting to as well.

Also, if you have two state machines sending messages to each other,
the question of whether those messages reside on a queue while in transit,
or any other detail of the implementation of their conveyance, is really
not in the scope of the state machine design itself.

### Inputs are always defined at some level of abstraction

For example, _mouse button depressed_ and _menu item selected_ are both events,
but the latter is at a higher level of abstraction than the former; indeed,
pressing the mouse button down may be one way of selecting a menu item
(while there might also be other ways, such as using keyboard navigation).
A state machine can exist at any level of abstraction, but typically exists
only at that one level; events from other levels usually need not be considered
in its design.

### State transitions are atomic

There's a simple proof by _reductio ad absurdum_ for this one: if state transitions
_weren't_ atomic, then you could introduce another state in the state diagram
that describes the intermediate state -- the state of the system while the transition
is taking place.  And, naturally, you would have transitions into and out of that
intermediate state.  But then, what would be stopping you from introducing
further intermediate states for _those_ transitions, and for the transitions into
those further intermediate states... and so on unendingly?  It would be an infinite
regress.  Therefore -- at the level of abstraction that the state machine is dealing
with -- transitions between states must be atomic.

### State machines can also describe lifecycles of objects

Traditionally, the subject of a state machine diagram is some kind of interactive
system, but many other kinds of objects undergo state transitions over time as well.
These tend to be on longer timescales.  For instance, a loan application
might be in one of the following states at any given time: being filled out,
submitted and waiting for evaluation, in evaluation, accepted, or rejected.

### Lifecycles tend towards linear, interactive systems tend towards cyclic

This should be apparent from the word "life", which implies birth and
death.

Often, state machine diagrams have distinguished notation for
"start state" and "end state".  These apply more strongly
to a lifecycle of an object than to an interactive system, where
the concept can be somewhat subjective.  (Is the start state of
a cardboard box the open state or the closed state?)

## *Statecharts*

### State machines have the potential for combinatorial explosion

Say you have an array of four on/off switches.  Each switch
can be in 2 possible states.  But the array considered as a whole
can be in 2 times 2 times 2 times 2 (= 16) possible states, and
each of these states transitions to 4 other states.
A state diagram that includes all these states and transitions
would be unwieldy -- more cumbersome than helpful.

### Combinatorial explosion can be mitigated through nesting and parallelizing

In the array example above, it's unlikely that a significant number
of those 16 states have any meaning, in the sense of influencing
what the next state should be based on a given input.  It's likely
that the states are, for the most part, treated homogeneously.  So it
behooves us to have a notation that captures this, instead of naively
treating all states equally.

In the Statecharts notation, for example, the array could be depicted with
each switch being its own 2-state state machine nested inside an orthogonal
region (that is, a parallel partition) of a single superstate representing the
entire array.

### Statecharts was introduced by David Harel in the 1980's

The original paper introducing Statecharts can be found here:
[Statecharts: A Visual Formalism for Complex Systems (Harel, 1987)](https://www.wisdom.weizmann.ac.il/~dharel/SCANNED.PAPERS/Statecharts.pdf) (PDF).

Statecharts has been a very influential notation for state machine design,
but continues to be often misunderstood and under-appreciated
(much like state machines themselves.)
Major contributions from it are _hierarchically nested states_ and
_orthogonal regions_ within a superstate.

### Statecharts was adopted into OMT

OMT (Object Modelling Technique) was a software engineering methodology
formulated in the late 1980's.  OMT promoted a 3-axis design, consisting of
structural, functional, and dynamic aspects.  For the notation for the dynamic
aspect, OMT adopted Statecharts.  They were originally going to use their
own tree-based notation for nested states, but decided that Statechart's
contour-based notation was a better choice.  Details can be found in bibliographic
notes of Section 5 of the book
[Object-oriented Modeling and Design (Rumbaugh et al, 1991)](https://archive.org/details/objectorientedmo00rumb)
(archive.org, borrowable online.))

### Statecharts went on into UML

UML (Unified Modelling Language) is a set of software engineering practices and notations
that grew out of the OMT and Booch formalisms.  One of the concepts that UML
provides is the [UML state machine](https://en.wikipedia.org/wiki/UML_state_machine) (Wikipedia),
which has been strongly influenced by Statecharts, supporting the same
major contributions: hierarchically nested states and orthogonal (i.e. parallel) regions.

## *Implementation*

### There are many ways to implement a state machine

In the words of SCTV's fictional Mayor Tommy Shanks, "There are so many ways to
implement a state machine, you could shake a stick at them."  The paper
[The Anthology of the Finite State Machine Design Patterns (Adamczyk, 2003(?))](https://www.hillside.net/plop/plop/plop2003/Papers/Adamczyk-State-Machine.pdf) (PDF)
lists dozens of such ways (mostly variations on the State Design Pattern).
Even outside of object-oriented designs, there are a number of choices
that can be made: to use a lookup table, to switch on state for a
given input, to switch on input for a given state, to have dedicated
input code in each state, and so forth.

### A state machine's implementation can closely resemble its design

Notwithstanding the previous fact, it is often possible to pick a
a straightforward implementation method and run with it.  With
prudent software design choices, the conceptual distance between the
design elements (states, transitions) and the implementation elements
(states, transitions) will be small.

This makes state machines all the more attractive because implementing
one is almost mechanical; and checking the implementation against the
specification is also made easier.
(The caveat of using the implementation itself *as* the specification
still applies, though: the code itself cannot tell you what the code
*should* do.)

### There are software libraries for implementing state machines

You may or may not benefit from using one.  Implementing a state
machine from scratch is not difficult, and it pays to choose
a software design (see the previous 2 facts) that fits your problem
space -- which a generic library might not provide.  So using a
library might be  less beneficial than you might imagine (certainly
less beneficial than e.g. a library for reading JPEGs -- something
that is difficult to implement and doesn't admit so much variation.)

### The states are often implemented as an enumeration

Lots of programming languages provide something like this; for example,
C has an `enum` type, and Haskell has a disjoint sum type (as part of
algebraic data types).  It's a good fit for the finite nature of the
set of control states; it makes for more readable source code, and
(in a type-checked setting) can prevent a state index variable from taking
on illegal value (that is, one that does not represent any state).

### Boolean flag creep introduces impossible states

State machines are sometimes said to be a remedy for architectural decay,
which means, in part, the tendency for a code base to grow a
new boolean flag every time a new condition is identified.  Suppose you're
writing a user interface.  You start with a basic implementation, then you
realize you need to wait until some backend service is ready.  So you add a flag,
`is_ready`.  Then you realize some operation might not succeed and you need
to signal the user of this.  So you add another flag, `is_error`.  Now,
you have the possibility of *both* of these flags being true.  But is that
a meaningful situation?  Probably it's not.  At this point it's best to
rethink the set of states your user interface can actually be in, and
formulate an enumeration that matches those states,
and use that enumeration instead of these individual boolean flags.

### You might find that some of the states are "derived states"

Suppose you are writing a billing system.  One of the requirements is
that when a new invoice is created, it has no line items.  Another of
the requirements is that it should not be possible to submit an empty
invoice.

So in the state machine, "Empty" and "Non-Empty" are modelled as states
the invoice can be in, and the "submit" input only has an effect in
the "Non-Empty" state, where it transitions to "Submitted".  This very
clearly illustrates the requirements.

But when implementing this state machine, it might not make
sense to formulate an enumeration with both "Empty" and "Non-Empty"
in it, because these conditions really depend on the number of lines the
invoice has -- a quantitative piece of state.  They're both instances
of a more general state, "Being Edited".

So this is a case where the implementation could diverge from how
the diagram is drawn.  Conceptually, "Empty" and "Non-Empty" are
distinct states, for clarity, but in the implementation, they are
implemented as "derived states" instead of parts of the
"enumerated state".  Alternately, you could adjust the diagram
to have a single state, and have the "submit" transition guarded
by the condition "line item count > 0".

See also "qualitative vs quantitative state", above.

## *Advanced*

### Logical statements about state machines can be decided by model checking

We can establish a set of propositions, where each proposition is true at some
states and false at the others.  We can then give formulas in temporal logic,
such as "there exists at some future a time when p and q will always be true",
and run a model-checking process on our state machine to see in which states
of our state machine the formula holds.

For more information of model checking using temporal logic, see, for example,
chapter 3 of
[Logic in Computer Science (Huth and Ryan, 2000)](https://archive.org/details/logicincomputers0000huth)
(archive.org, borrowable online).

This comes down to the fact that temporal logic is a specialization of _modal logic_;
state machines are close relatives of _labelled transition systems_; and
modal logics are a natural (or could we say supernatural!) fit with labelled
transition systems.  For more on this view see, for example,
[First Steps in Modal Logic (Popkorn, 1994)](https://archive.org/details/firststepsinmoda0000popk)
(archive.org, borrowable online).

### Nesting state machines enables a kind of modularity

Suppose, in the spirit of modularity, we want some part of our state
machine to be "pluggable": we want to be able to swap it out for an
alternate implementation of that part, one that behaves differently
in some ways but is still overall compatible with the rest of the state machine.

For this to work, a modularity boundary must be established around this
part.  As long as whatever is inside the boundary reacts like everything
outside the boundary expects, those insides can be swapped out for other
insides that meet the same expectations.

If those insides have their own reactive behaviour, which they probably
do, then the best way to model this is to put the modularity boundary
around a single superstate, which has its own substates (basically its
own sub-state machine.)

For this to work, the substates must be "private"; everything outside
the modularity boundary must not rely on knowledge of them, lest
problems pop up when we try to swap out the superstate with one that
has different substates.

### The "History pseudo-state" can be avoided by use of a convention

Statecharts defines a "history state" (capital H in a circle).
Its is more than a little confusing but, from what I can tell, it is
not actually necessary in many situations, especially if one adopts the following
default behavior:

When re-entering a state _s_ that contains substates, the current substate among
those substate is the same one that was current when _s_ was previously left.

If _s_ was never previously left, then one must consult the start state(s) inside
_s_ to discover which the current substate.

So this is sort of a "history by default" approach.  _If_ one wished to transition
from some outside state into a specific substate of _s_, one may do so by having
a transition arrow go, not to _s_, but directly to the desired substate.

Transitions directly into substates like this can be very
useful, but do note they violate the "privacy" requirement of the previous
fact, so they work against modularity (which might or might not be a problem,
depending on the situation.)

An alternate approach to account for modularity might be to decorate
arrows transitioning to _s_ with side-effects such as "Reset _s_ to its
start substate" instead of having them transition to a substate inside _s_.

### State machines are neither imperative nor functional

When the machine switches states, did it destructively update the current
state of the system, or did it create a new state of the system and switch to
that new state?  You can implement it either way.  The state machine itself
doesn't care.

### State machines demonstrate a weakness of toggling

Suppose we have bursts of events -- sometimes you don't just get one event,
you get a bunch of them.  Physical contact switches are like this -- the
phenomenon is called "bounce".

Suppose further that we have 2 states, On and Off, and a "toggle" input that
transitions both from On to Off and from Off to On.  If it receives a burst
of "toggle" inputs, it is not possible to predict which state it will end
up in.

But suppose instead we have 2 inputs, "turn on" and "turn off", each of
which transitions from only one state to the other.  Now, if we get a
burst of "turn on" (resp. "turn off"), we know what state we will always
end up in: On (resp Off).

There are other situations similar to bursts, e.g. simply not being
aware of which state you are currently in, so this informs good design.

