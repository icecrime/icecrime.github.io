---
layout: post
title: "A structured approach to labeling"
description: "How to scale items classification using labels."
tags: [organization, tooling, open-source]
categories: [Technology]
---

Everything these days have labels: emails, GitHub issues and pull requests, todo list items, saved articles, etc. More importantly, labels often are the _only_ available tool for classification. Yet, bad labels can increase clutter and confuse more than they inform.

In this post I'll make a case for structuring labels, using GitHub issues and pull requests labels as an example.

# Sending the right message

## One label, two meanings

It's often underlooked that a label has _two_ meanings: one when it's applied, and one when it isn't. A label adds a piece of information not only to items that bear it, but also by contrast to items which don't. One striking example is the `help wanted` label on GitHub: using this label on any subset of items conveys (deliberately or not) that help is _not_ desired on the others.

Take the time to consider the implicit classification of unlabeled items. When `help wanted` exists as a label, the default situation is implicitly that help isn't wanted. Rename this label to `help not needed` and you just reversed that perception. Such details may be of importance when aiming to build a welcoming project.

## The label soup

The default set of labels on GitHub is the following: `bug`, `duplicate`, `enhancement`, `help wanted`, `invalid`, `question`, `wontfix`.

The problem with a flat collection of labels is that there's no obvious purpose, and no explicit relationship between them. For example, which labels are mutually exclusive? It might be generally accepted that an issue is _either_ a `bug` or an `enhancement`, but what about `question`? Can I have a `bug question` and an `enhancement question`? What about a `invalid question`?

<figure class="center">
    <a href="/images/2017-03-24-labels/alphabet_soup_help.jpeg"><img src="/images/2017-03-24-labels/alphabet_soup_help.jpeg" alt=""></a>
</figure>

A flat collection of labels is an heterogenous pool of values to pick from: like anything which doesn't have clear intent, it becomes subject to interpretation. Luckily, we have a nice tool to give meaning to values: types!

# A structured approach to labeling

## Thinking with types

If you were writing code, how would you define a type to hold the metadata you care about? Taking an imaginary set of labels as an example, this is what the typical label organization would look like when expressed as code:

```go
type Label int

const (
    API Label = iota
    Bug
    CodeReview
    DesignReview
    Networking
    Question
    Storage
)

type Metadata []Label
```

*For those unfamiliar with Go, this is simply defining a `Label` enumerate, and the `Metadata` type as a collection of `Label` values.*

That's the "label soup" described above, but we can be more expressive about the intent and constraints:

```go
type Area int

const (
	API Area = iota
	Networking
	Storage
)

type Kind int

const (
	Bug Kind = iota
	Feature
	Question
)

type Status int

const (
	DesignReview Status = iota
	CodeReview
)

type Metadata struct {
	Areas  []Area
	Kind   Kind
	Status Status
}
```

The `Metadata` type properly captures that a given item can have multiple _areas_, a single _kind_, and a single _status_. Similarly, it's now clear that an item is _either_ a `Bug`, a `Feature`, or a `Question`.

## Expressing as labels

Now armed with the model we want, we need a way to represent it with labels. Labels are typically just strings, so we need some kind of micro-format: the way it's set up on the [Docker project](https://github.com/docker/docker/labels) and what I use throughout my tools is a straightforward `field/value` syntax.

| Area               | Kind             | Status                 |
|:-------------------|:-----------------|:-----------------------|
| `areas/api`        | `kind/bug`       | `status/design-review` |
| `areas/networking` | `kind/feature`   | `status/code-review`   |
| `areas/storage`    | `kind/question`  |                        |

This gives us quite a different approach to labeling: **setting a label is assigning a value to a named field of a metadata type**. The intended structure:

```go
Metadata{
    Areas:  []Area{ API, Networking },
    Kind:   Bug,
    Status: CodeReview,    
}
```

... translates to the following set of labels: `areas/api`, `areas/networking`, `kind/bug`, `status/code-review`. Easy enough!

Of course, none of the services I know would _technically_ enforce that an item can have multiple `areas/` but a single `kind/`. The best we can do is rely on the added explicit purpose on each label, and on the pluralization of `areas/` field name to signify a list over a scalar value. On the Docker project, we took the extra step of [documenting](https://github.com/docker/docker/blob/master/project/ISSUE-TRIAGE.md#2-classify-the-issue) the labels.

As a bonus: structured labels make it way easier to visualize data according to specific attributes. For example breaking down GitHub issues into `areas`, `kind`, and `version`:

<figure class="center">
    <a href="/images/2017-03-24-labels/issues_breakdown.png"><img src="/images/2017-03-24-labels/issues_breakdown_crop.png" alt=""></a>
    <figcaption><a href="/images/2017-03-24-labels/issue_breakdown.png" title="Issues breakdown">Issues breakdown</a>.</figcaption>
</figure>

# Summing up

Whether on GitHub issues, emails, todo list tasks, or unread articles, labels are often are only tool provided for classification, and getting them right is key to being able to manage large sets of items. Take the time to consider their explicit and implicit meanings, and how much is subject to interpretation. A structured approach to labeling can truly help here.

As the implementer of a service that supports labels, define the default set wisely. And if it happens that your service is targeted at a technical audience, I think it's worth exploring how a labeling system could embrace a structured approach and offer the ability to specify a model in order to enforce constraints.