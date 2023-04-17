# The Little Schemer

[TOC]

# 1. Toys (Basic concepts of the Scheme Language)

## Basic construction

### Atom

Every existed single object in the real world is [Atom](#atom).

### List

A collection of S-expression enclosed by parentheses is [List](#list).

> - A list can be empty, but also be a [List](#list).

## Action on list

### car & cdr

Both of them are defined as map from [List]() to [Atom]().

The [car](#car) try to get the first [atom](#atom) of the list it acts. 

The [cdr]() try to get the list removed the first [atom](#atom). 

> - The action of Car on an empty list is not defined. In Lisp, it will get [nil]().
> - Remove the only one atom will get an empty list.