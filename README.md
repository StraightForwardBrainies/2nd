# 2nd
def setStatus(self,v, val): 
 self.status[v]=val 
 def getHeuristicNodeValue(self, n):
 return self.H.get(n,0) # always return the heuristic value of a given node 
 def setHeuristicNodeValue(self, n, value):
 self.H[n]=value
 def printSolution(self):
 print("FOR GRAPH SOLUTION, TRAVERSE THE GRAPH FROM THE START 
NODE:",self.start)
 print("------------------------------------------------------------")
 print(self.solutionGraph)
 print("------------------------------------------------------------")

 def computeMinimumCostChildNodes(self, v): 
 minimumCost=0
 costToChildNodeListDict={}
 costToChildNodeListDict[minimumCost]=[]
 flag=True
 for nodeInfoTupleList in self.getNeighbors(v):
 cost=0
 nodeList=[]
 for c, weight in nodeInfoTupleList:
 cost=cost+self.getHeuristicNodeValue(c)+weight
 nodeList.append(c) 
 if flag==True: 
 minimumCost=cost
 costToChildNodeListDict[minimumCost]=nodeList 
 flag=False
 else:
 if minimumCost>cost:
 minimumCost=cost
 costToChildNodeListDict[minimumCost]=nodeList 
 return minimumCost, costToChildNodeListDict[minimumCost] 
 def aoStar(self, v, backTracking): 
 print("HEURISTIC VALUES :", self.H)
 print("SOLUTION GRAPH :", self.solutionGraph)
 print("PROCESSING NODE :", v)
 
print("-----------------------------------------------------------------------------------------")
 if self.getStatus(v) >= 0: # if status node v >= 0, compute Minimum Cost nodes of v
 minimumCost, childNodeList = self.computeMinimumCostChildNodes(v)
 self.setHeuristicNodeValue(v, minimumCost)
 self.setStatus(v,len(childNodeList)) 
 solved=True 
 self.parent[childNode]=v
 if self.getStatus(childNode)!=-1:
 if solved==True: 
 self.setStatus(v,-1) 
 self.solutionGraph[v]=childNodeList 
 if v!=self.start:   
 self.aoStar(self.parent[v], True) 
 if backTracking==False: 
 self.setStatus(childNode,0) 
 self.aoStar(childNode, False)  
 
h1 = {'A': 1, 'B': 6, 'C': 2, 'D': 12, 'E': 2, 'F': 1, 'G': 5, 'H': 7, 'I': 7, 'J': 1, 'T': 3}
{
 'A': [[('B', 1), ('C', 1)], [('D', 1)]],
 'B': [[('G', 1)], [('H', 1)]],
 'C': [[('J', 1)]],
 'D': [[('E', 1), ('F', 1)]],
 'G': [[('I', 1)]] 
}
h2 = {'A': 1, 'B': 6, 'C': 12, 'D': 10, 'E': 4, 'F': 4, 'G': 5, 'H': 7}
 {
 'A': [[('B', 1), ('C', 1)], [('D', 1)]], 
 'B': [[('G', 1)], [('H', 1)]], 
 'D': [[('E', 1), ('F', 1)]] 
}

h3 = {'A': 1, 'B': 5, 'C': 3, 'D': 18, 'E': 4, 'F': 0, 'G': 0, 'H': 0,'I':0} 
 { 
 'A': [[('B', 1), ('C', 1)], [('D', 1)]], 
 'B': [[('E', 1),('F', 1)]], 
 'C': [[('H', 1)]],
 'E':[[('G', 1)]], 
 'D': [[('I', 1)]]
}
G2 = Graph(graph3, h3, 'A')
G2.applyAOStar()
