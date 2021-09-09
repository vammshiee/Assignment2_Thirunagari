# Assignment2_Thirunagari
Assignment Two begins.
# Vamshi Krishna Thirunagari # 
### Saroornagar park in Hyderabad India ###
The saroornagar park is the one of the most famous tourist spot in southern india.I like the park because it is located on the bank of the **lake sarooornagar**.Local people call it as **saroornagar katta** .It is the beautiful place to hang around.
<hr/>

### Directions to saroornagar park from Maryville ###

1. Book a cab to KC airport from Maryyville
2. take a flight to new york for international travel
3. After reaching New york Airport,we must follow  below steps
   1. take a flight to india
   2. pass the immigration test
   3. after reaching delhi ,take a bus to hyderabad
   4. In Hyderabad book an uber cab to saroornagar park
   5. buy an entry ticket
4. Finally we have reached our destination .

#### Items that needs to be brought to Favorite Place ####
* Frisbee
* Cricket Gear
   * ball
   * bat
   * wickets
* Water
* Food
* Music Player
* Tent for campaign

[My Info](AboutMe.md) 

---

# Foods/drinks you should try once in a life time
The given table  informs us about the best food that i have come across in my lifetime.
 
| Food/Drink | Location | Price |
|------------|--------|------|
|   Butter Naan  | Saroornagar   | $1 |
|   Falooda   | Dilsukhnagar| $2 |
|   vada pav     | karmanghat | $5 |
|   pav Bhaji     | Malakpet | $4 |


---

# Pithy Quotes

> The best and most beautiful things in the world cannot be seen or even touched — they must be felt with the heart. -Helen Keller
> 
> Whoever is happy will make others happy too. -Anne Frank

---

# Convex Hull construction using Graham's Scan

> Graham's scan is a method of finding the convex hull of a finite set of points in the plane with time complexity O(n log n). It is named after Ronald Graham, who published the original algorithm in 1972. The algorithm finds all vertices of the convex hull ordered along its boundary.Reference found on this link <https://en.wikipedia.org/wiki/Graham_scan#:~:text=Graham's%20scan%20is%20a%20method,hull%20ordered%20along%20its%20boundary.>

```
struct pt {
    double x, y;
};

bool cmp(pt a, pt b) {
    return a.x < b.x || (a.x == b.x && a.y < b.y);
}

bool cw(pt a, pt b, pt c) {
    return a.x*(b.y-c.y)+b.x*(c.y-a.y)+c.x*(a.y-b.y) < 0;
}

bool ccw(pt a, pt b, pt c) {
    return a.x*(b.y-c.y)+b.x*(c.y-a.y)+c.x*(a.y-b.y) > 0;
}

void convex_hull(vector<pt>& a) {
    if (a.size() == 1)
        return;

    sort(a.begin(), a.end(), &cmp);
    pt p1 = a[0], p2 = a.back();
    vector<pt> up, down;
    up.push_back(p1);
    down.push_back(p1);
    for (int i = 1; i < (int)a.size(); i++) {
        if (i == a.size() - 1 || cw(p1, a[i], p2)) {
            while (up.size() >= 2 && !cw(up[up.size()-2], up[up.size()-1], a[i]))
                up.pop_back();
            up.push_back(a[i]);
        }
        if (i == a.size() - 1 || ccw(p1, a[i], p2)) {
            while(down.size() >= 2 && !ccw(down[down.size()-2], down[down.size()-1], a[i]))
                down.pop_back();
            down.push_back(a[i]);
        }
    }

    a.clear();
    for (int i = 0; i < (int)up.size(); i++)
        a.push_back(up[i]);
    for (int i = down.size() - 2; i > 0; i--)
        a.push_back(down[i]);
}
```
[Link to the above code](https://cp-algorithms.com/geometry/grahams-scan-convex-hull.html)