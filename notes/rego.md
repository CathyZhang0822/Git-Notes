# Rego 
https://www.openpolicyagent.org/docs/latest/policy-language/#why-use-rego   
OPA: Open Policy Agent   
Rego是OPA的native query language   


## Scalar Vlues
Scalar values are the simplest type of term in Rego. Scalar values can be Strings, numbers, booleans or null.   
```rego
greeting   := "Hello"
max_height := 42
pi         := 3.14159
allowed    := true
location   := null
```
These documents can be queried like any other:   
`[greeting, max_height, pi, allowed, location]`
```rego
[
  "Hello",
  42,
  3.14159,
  true,
  null
]
```

## Composite Values
Composite values define collections. 
```rego
cube := {"width": 3, "height": 4, "depth": 5}
```
The resulf:   
```
cube.width
```
`3`
Composite values can also be defined in terms of **Variables** or **References**(Variable和). For example:   
```rego
a := 42
b := false
c := null
d := {"a": a, "x": [b, c]}
```
```
+----+-------+------+---------------------------+
| a  |   b   |  c   |             d             |
+----+-------+------+---------------------------+
| 42 | false | null | {"a":42,"x":[false,null]} |
+----+-------+------+---------------------------+
```
### Objects
Objects are unordered key-value collections. In Rego, any value type can be used as an object key. For example, the following assignment maps port numbers to a list of IP addresses.   
```rego
ips_by_port := {
    80: ["1.1.1.1", "1.1.1.2"],
    443: ["2.2.2.1"],
}
```
```rego
ips_by_port[80]
```
```
[
  "1.1.1.1",
  "1.1.1.2"
]
```
```
some port; ips_by_port[port][_] == "2.2.2.1"
```
```
+------+
| port |
+------+
| 443  |
+------+
```
### Sets
In addition to arrays and objects, Rego supports set values. Sets are unordered collections of unique values. Just like other composite values, sets can be defined in terms of scalars, variables, references, and other composite values. For example:   
```rego
s := {cube.width, cube.height, cube.depth}
```
```rego
{1,2,3} == {3,1,2}
```
```
true
```
## Variables ???看不懂doc












