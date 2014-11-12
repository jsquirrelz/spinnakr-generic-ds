### Spinnakr Rule Spec

All of the rule data will live in Redis. Rules are account and project specific thus stored on the Accounts unique DB.

Below is a list the keys used for rules:

#### Generic Persistence Keys

```
rules-primary-key
```
A key that is incremented on every rule creation. Used as a unique identifier for rules.

```
set:PROJECT:rules
```
Contains a set of rule keys for the specific project. Keys can be added and removed.

#### Rule Key

```
hash:PROJECT:EVENT_TYPE:rule:ID
```

The generic key structure for rules.

Every rule belongs to a project and has an `EVENT_TYPE`.

`EVENT_TYPE` can either be:
- `comparator`
- `observer`

The contents of the keys can vary depending on the `EVENT_TYPE` but
all keys should have `dimension`, `key`, and `interval`. 

Specifc keys `comparator` should contain are `calculation`, `threshold`, and `result`.

A full example would be:

```
1) "dimension" 
2) "job-skills"
3) "key"
4) "ruby"
5) "calculation"
6) "sum"
7) "threshold"
8) "10"
9) "result"
10) "equal"
11) "interval"
12) "weeks"
```


Specifc keys `observer` should contain are `watch`, and `trigger`.

A full example would be:

```
1) "dimension" 
2) "job-skills"
3) "key"
4) "ruby"
5) "watch"
6) "keys"
7) "trigger"
8) "10"
9) "interval"
10) "days"

```