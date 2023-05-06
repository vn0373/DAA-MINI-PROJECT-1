#BRUTE FORCE APPROACH

vector<pair<int, int>> getSkyline(vector<vector<int>>& buildings) {
vector<pair<int, int>> result;
int n = buildings.size();
for (int i = 0; i < n; i++) {
int x1 = buildings[i][0];
int x2 = buildings[i][1];
int h = buildings[i][2];
for (int j = x1; j <= x2; j++) {
int max_height = 0;
for (int k = 0; k < n; k++) {
if (buildings[k][0] <= j && buildings[k][1] >= j) {
max_height = max(max_height, buildings[k][2]);
}
}
result.push_back(make_pair(j, max_height));
}
}
return result;
}

#DIVIDE AND CONQUER

vector<pair<int, int>> getSkyline(vector<vector<int>>& buildings) {
vector<pair<int, int>> result;
int n = buildings.size();
for (int i = 0; i < n; i++) {
int x1 = buildings[i][0];
int x2 = buildings[i][1];
int h = buildings[i][2];
for (int j = x1; j <= x2; j++) {
int max_height = 0;
for (int k = 0; k < n; k++) {
if (buildings[k][0] <= j && buildings[k][1] >= j) {
max_height = max(max_height, buildings[k][2]);
}
}
result.push_back(make_pair(j, max_height));
}
}
return result;
}


# PROBABLITY QUEUE

vector<pair<int, int>> getSkyline(vector<vector<int>>& buildings) {
vector<pair<int, int>> result;
int n = buildings.size();
if (n == 0) {
return result;
}
priority_queue<pair<int, int>> heights;
int i = 0, x = 0, y = 0;
while (i < n || !heights.empty()) {
if (heights.empty() || (i < n && buildings[i][0] <= heights.top().second)) {
x = buildings[i][0];
while (i < n && buildings[i][0] == x) {
heights.push(make_pair(buildings[i][2], buildings[i][1]));
i++;
}
} else {
x = heights.top().second;
while (!heights.empty() && heights.top().second <= x) {
heights.pop();
}
}
y = (heights.empty() ? 0 : heights.top().first);
if (result.empty() || result.back().second != y) {
result.push_back(make_pair(x, y));
}
}
return result;
}
