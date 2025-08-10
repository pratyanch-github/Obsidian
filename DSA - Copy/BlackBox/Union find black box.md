also know as dsu, 

hamare paas kuch elements(nodes) diye hote hai, nodes ke beech me link(connection) ho sakta hai,  inhi elements ke group ko set bolte hai , har set me ek representative(ultimate parent) hota hai,

so dsu , ye kuch nahi bas ek array hai jisme initially sare elements ke ultimate parent wo khud hi hai , matlab initially hamare paas n number of sets hai aur har set me ek hi element hai, 

ham do sets ko combine kar sakte hai , iska matalab agar hamare paas set A and set B hai to set A ke kisi bhi element ko agar set B ke kisi bhi element se connect hona ho,  iske liye hame dono set ke representative elements find karna hoga aur unke bech ek link(connection ) create karna hoga, i.e   parent[representative of A ] = representative of B 
ya   parent[representative of B ] = representative of A


we have 3 apis 

- `make_set(v)` - creates a new set consisting of the new element `v`
- `union_sets(a, b)` - merges the two specified sets (the set in which the element `a` is located, and the set in which the element `b` is located)
- `find_set(v)` - returns the representative (also called leader) of the set that contains the element `v`. This representative is an element of its corresponding set. It is selected in each set by the data structure itself (and can change over time, namely after `union_sets` calls). This representative can be used to check if two elements are part of the same set or not. `a` and `b` are exactly in the same set, if `find_set(a) == find_set(b)`. Otherwise they are in different sets.

```
void make_set(int v) {
    parent[v] = v;
}

int find_set(int v) {
    if (v == parent[v])
        return v;
    return find_set(parent[v]);
}

void union_sets(int a, int b) {
    a = find_set(a);
    b = find_set(b);
    if (a != b)
        parent[b] = a;
}
```