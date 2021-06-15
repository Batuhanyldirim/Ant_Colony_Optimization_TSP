

"""
This code Solves the Travelers Salesman Problem by using Ant Colony Optimization.
"""

f = open("/content/Assignment 3 berlin52.txt", "r")

lines = f.readlines()

berlin = {}

for i in lines[6:-2]:# creates graph in a dictionary from text file
  line = i.split(" ")
  berlin[line[0]] = [float(line[1]),float(line[2])]

for i in berlin:
  print(i,berlin[i])

k = berlin.keys()
global cit
cit = []

for i in k:
  cit.append(i)

print(cit)


import random
import math
import numpy as np



global alp
global bet
global evop


global ants
global feremone
global heuristic

global best
global current_best

pop_size = 5

path_len = 52

evop = (1 - 0.9)

alp = 0.7
bet = 0.8


def create_feremone_tab():
  global feremone
  for i in range(path_len):
    row = []
    for k in range(i):
      row.append(-1)
    for j in range(i,path_len):
      if i == j:
        row.append(-1)
      else:
        row.append(1)
    feremone.append(row.copy())

def create_heuristic_tab():
  global heuristic
  for i in range(path_len):
    row = []
    for k in range(i):
          row.append(-1)
    for j in range(i,path_len):
      if i == j:
        row.append(-1)
      else:
        x = abs(float(berlin[str(i+1)][0]) - float(berlin[str(j+1)][0]))
        y = abs(float(berlin[str(i+1)][1]) - float(berlin[str(j+1)][1]))
        dist = 1/float(math.sqrt((x*x)+(y*y)))
        row.append(dist)
    heuristic.append(row.copy())


def fitness(ind):
  sum = 0
  for i in range(52):
    x = abs(float(berlin[ind[0][i]][0]) - float(berlin[ind[0][i+1]][0]))
    y = abs(float(berlin[ind[0][i]][1]) - float(berlin[ind[0][i+1]][1]))
    dist = math.sqrt((x*x)+(y*y))
    sum += dist
  return sum

def initialize_ants(pop_size):
  global cit
  cit = cit + ['1']
  # example initial ant = [cit,cost]
  cost = fitness([cit,0])
  global ants
  for i in range(pop_size):
    ants.append([cit.copy(),cost])
  cit.pop()


def cal_fer(cit_a, cit_b):
  if int(cit_a) > int(cit_b):
    return feremone[int(cit_b)-1][int(cit_a)-1]
  else:
    return feremone[int(cit_a)-1][int(cit_b)-1]

def cal_her(cit_a,cit_b):
 
  if int(cit_a) > int(cit_b):
    return heuristic[int(cit_b)-1][int(cit_a)-1]
  else:
    return heuristic[int(cit_a)-1][int(cit_b)-1]


def chose_path(ant,idx):
  global cit
  global alp
  global bet
  probs = []
  unvisited = []
  available = cit.copy()

  for i in ant[0][:idx]:
    available[int(i)-1] = '-1'
  for i in range(1,53):
    if available[i-1] != '-1' and ant[0][idx] != available[i-1]:
      unvisited.append(available[i-1])
      denom = 0
      fer = cal_fer(ant[0][idx],available[i-1])
      her = cal_her(ant[0][idx],available[i-1])
      num = pow(fer,alp)*pow(her,bet)
      for j in range(52):
        if available[j] != '-1' and ant[0][idx] !=available[j]:
          fer = cal_fer(ant[0][idx],available[j])
          her = cal_her(ant[0][idx],available[j])
          if fer == 0:
            fer = 0.00001
          denom += float(pow(fer,alp)*pow(her,bet))
      if denom == 0:
        print("ant[0][idx]:",ant[0][idx])
        print("available[i-1]:",available[i-1])
        print("fer:",fer)
        print("her:",her)
        print("num:",num)
        print("denom:",denom)
        print("available:",available)
        print()
        input()

      prob = num/float(denom)
      probs.append(prob)
  
  """print("ant:",ant)
  print("idx:",idx)
  print("unvisited:",unvisited)
  print("probs:",probs)"""
    
  
  if unvisited:
    res = random.choices(unvisited, weights=probs, k=1)[0]#np.random.choice(unvisited,1,probs)[0]
    """print("unvisited:",unvisited)
    print("probs:",probs)
    print("Highest prob:",max(probs))
    print("Highest city idx:",probs.index(max(probs)))
    print("Max prob city:",unvisited[probs.index(max(probs))])
    print("chosen city:",res)
    input()"""
    return  res
  else:
    return '1'
  




def solution(path_len):
  global ants
  for i in range(path_len):
    for j in range(pop_size):
      ants[j][0][i+1] = chose_path(ants[j],i)




def cal_total_cost():
  global pop_size
  global best
  global ants
  global current_best

  current_best = ants[0]
  for i in range(pop_size):
    ants[i][1] = fitness(ants[i])

    if ants[i][1] < current_best[1]:
      current_best = [ants[i][0].copy(),ants[i][1]]

    if ants[i][1] < best[1]:
      best = [ants[i][0].copy(),ants[i][1]]

def update_pher():
  global feremone
  global evop
  global ants
  for i in range(path_len):
    for j in range(i,path_len):
      if i != j:
        feremone[i][j] *= evop
  
  for ant in ants:
    for i in range(52):
      x = abs(float(berlin[ant[0][i]][0]) - float(berlin[ant[0][i+1]][0]))
      y = abs(float(berlin[ant[0][i]][1]) - float(berlin[ant[0][i+1]][1]))
      dist = math.sqrt((x*x)+(y*y))
      first = int(ant[0][i])
      second = int(ant[0][i+1])
      if first > second:
        feremone[second-1][first-1] += 1/float(dist)
      elif first < second:
        feremone[first-1][second-1] += 1/float(dist)

  for i in range(52):
    x = abs(float(berlin[best[0][i]][0]) - float(berlin[best[0][i+1]][0]))
    y = abs(float(berlin[best[0][i]][1]) - float(berlin[best[0][i+1]][1]))
    dist = math.sqrt((x*x)+(y*y))
    first = int(best[0][i])
    second = int(best[0][i+1])
    if first > second:
      feremone[second-1][first-1] += 1/float(dist)
    elif first < second:
      feremone[first-1][second-1] += 1/float(dist)
     

  






"""for i in feremone:
  print(i)
"""
def ACO(j,succ):
  global best
  global current_best
  global ants
  global feremone
  global heuristic
  ants = []
  feremone = []
  heuristic = []
  create_feremone_tab()
  create_heuristic_tab()
  initialize_ants(pop_size)
  best = [ants[0][0].copy(),fitness(ants[0])]
  for i in range(150):
    solution(path_len)
    cal_total_cost()
    update_pher()
    print("Iteration(",j,")",i+1)
    print("succ:",succ)
    print("Best Ant:",best )
    print("Best Score:",best[1])
    print("Current best ant:",current_best)
    print("Current best score:", current_best[1])
    print("\n")
  return best[1]



























