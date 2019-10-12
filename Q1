import sys
import math
earth_radius = 6371
class travel_graph:
    def __init__(self):
        self.start_place = ""
        self.end_place = ""
        self.gas_distance = 0
        self.graph = {}
        self.city_dict = {}
        self.dist_dict = {}
        self.prev_dict = {}
    def get_path(self):
        a_list = []
        current_place = self.end_place
        while current_place != self.start_place:
            a_list.append(current_place)
            current_place = self.prev_dict[current_place]
            if current_place is None:
                return False
        a_list.append(self.start_place)
        a_list.reverse()
        return a_list
    def get_graph(self):
        for k in self.city_dict:
            self.graph[k] = []
            for i in self.city_dict:
                d = self.get_distance(k, i)
                if d != 0 and d != -1:
                    self.graph[k].append([i,d])
    def dijkstra(self):
        q = []
        for k in self.city_dict.keys():q.append(k)
        self.dist_dict[self.start_place] = 0
        while q:
            u = None
            for k in q:
                if u is None or self.dist_dict[k] < self.dist_dict[u]: u = k
            q.remove(u)
            if u == self.end_place:return
            for i in self.graph[u]:
                alt = self.dist_dict[u] + i[1]
                if alt < self.dist_dict[i[0]]:
                    self.dist_dict[i[0]] = alt
                    self.prev_dict[i[0]] = u

    def get_distance(self, x, y):
        d_lat = self.city_dict[y][0] - self.city_dict[x][0]
        d_lng = self.city_dict[y][1] - self.city_dict[x][1]
        a = math.sin(math.radians(d_lat/2))*math.sin(math.radians(d_lat/2)) + math.cos(math.radians(self.city_dict[x][0])) * math.cos(math.radians(self.city_dict[y][0])) * math.sin(math.radians(d_lng/2))*math.sin(math.radians(d_lng/2))
        c = 2 * math.atan2(math.sqrt(a), math.sqrt(1 - a))
        d = earth_radius * c
        if d > self.gas_distance:
            return -1
        return d
    def empty(self):
        self.city_dict = {}
        self.end_place = ""
        self.start_place = ""
        self.gas_distance = 0
        self.graph = {}
        self.dist_dict = {}
        self.prev_dict = {}
    def read(self,txt_input):
        self.empty()
        Num_cities = int(txt_input.readline())
        a_list = txt_input.readline().split()
        a_string = ' '.join(map(str,a_list[2:]))
        self.start_place = a_string
        self.city_dict[a_string] = [float(a_list[0]), float(a_list[1])]
        self.dist_dict[a_string] = 99999
        self.prev_dict[a_string] = None
        for i in range(Num_cities - 2):
            a_list = txt_input.readline().split()
            a_string = ' '.join(map(str,a_list[2:]))
            self.city_dict[a_string] = [float(a_list[0]),float(a_list[1])]
            self.dist_dict[a_string] = 99999
            self.prev_dict[a_string] = None
        a_list = txt_input.readline().split()
        a_string = ' '.join(map(str,a_list[2:]))
        self.end_place = a_string
        self.city_dict[a_string] = [float(a_list[0]), float(a_list[1])]
        self.dist_dict[a_string] = 99999
        self.prev_dict[a_string] = None
        self.gas_distance = float(txt_input.readline())




txt_input = sys.stdin
number_of_cases = int(txt_input.readline())
graph = travel_graph()

for i in range(number_of_cases):
    graph.read(txt_input)
    graph.get_graph()
    graph.dijkstra()
    path = graph.get_path()
    if path:
        for i in range (len(path)):
            if i == len(path) - 1:
                print(path[i])
            else:
                print(path[i]+", " ,end = "")
    else:
        print("Not possible")
