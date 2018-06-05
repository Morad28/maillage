#Differentes bibliothèques utilisées

from __future__ import division 
import matplotlib.pyplot as plt 
from random import *
import numpy as np



def maillage_carre(n,m):
    X=[x/(n-1) for x in range(n)]
    Y=[y/(m-1) for y in range(m)]
    N=n*m
    NP=[]       #Va contenir les numéros associés aux points 
    i,j,k=1,1,2
    T=[]        #Va contenir les numéros des triangles associés à leurs points
    T_sup=[]
    T_inf=[]
    for y in Y:
        for x in X:
            NP=NP+[[i,(x,y)]]       #On assosie à chaque point un numéro
            i=i+1
    
    for l in range(1,N-n,n):        
        for i in range(l,l+n-1):
            T_sup=T_sup+[(i,i+n,i+n+1)]     #Comme on numérote les points de gauche à droite en partant du bas
            T_inf=T_inf+[(i,i+1,i+n+1)]     #On a une relation etre le triangle i et ses points, en distingant 
                                            #les triangles supérieurs et inférieurs
    for t in T_sup:
        T=T+[[j,t]]                         #On associe aux triangles leur numéro
        j=j+2
    for t in T_inf:
        T=T+[[k,t]]
        k=k+2
    T=sorted(T)
    
    for i in range(m):
        plt.plot([0,1],[i/(m-1),i/(m-1)],c="b")         #On construit le quadrillage du carré unité
    for i in range(n):
        plt.plot([i/(n-1),i/(n-1)],[0,1],c="b")
    plt.axis("equal")
    
    lt=len(T)
    for i in range(lt):
        p1,p2,p3=T[i][1]
        x1,x2,x3=NP[p1-1][1][0],NP[p2-1][1][0],NP[p3-1][1][0]       #On construit les triangles
        y1,y2,y3=NP[p1-1][1][1],NP[p2-1][1][1],NP[p3-1][1][1]
        plt.triplot([x1,x2,x3],[y1,y2,y3])
    plt.show()
    return(T)

def maillage_carre(n,m):            #Une autre version avec une numérotation des points et triangles implicite
    X=[x/(n-1) for x in range(n)]
    Y=[y/(m-1) for y in range(m)]
    N=n*m
    NP=[]       #Va contenir les numéros associés aux points 
    
    T=[]        #Va contenir les numéros des triangles associés à leurs points
    T_sup=[]
    T_inf=[]
    for y in Y:
        for x in X:
            NP=NP+[[x,y]]       #On assosie à chaque point un numéro
            
    
    for l in range(1,N-n,n):        
        for i in range(l,l+n-1):
            T_sup=T_sup+[[i,i+n,i+n+1]]     
            T_inf=T_inf+[[i,i+1,i+n+1]]      
                                            
    T=T_sup+T_inf
    for i in range(m):
        plt.plot([0,1],[i/(m-1),i/(m-1)],c="b")         #On construit le quadrillage du carré unité
    for i in range(n):
        plt.plot([i/(n-1),i/(n-1)],[0,1],c="b")
    plt.axis("equal")
    
    lt=len(T)
    for i in range(lt):
        p1,p2,p3=T[i]
        x1,x2,x3=NP[p1-1][0],NP[p2-1][0],NP[p3-1][0]       #On construit les triangles
        y1,y2,y3=NP[p1-1][1],NP[p2-1][1],NP[p3-1][1]
        plt.triplot([x1,x2,x3],[y1,y2,y3])
    plt.show()
    return(T,NP)

def aretes(L):
    A=[]
    for p in range(len(L)):
        i,j,k=L[p][1]
        A=A+[[[i,j],[j,k],[k,i]]]
    return(A)


def nuage(N,xmin,xmax,e):
    L=[np.array([xmin+(xmax-xmin)*random(),xmin+(xmax-xmin)*random()])]
    X=[]
    Y=[]
    j=0
    for j in range(N):
        x,y=xmin+(xmax-xmin)*random(),xmin+(xmax-xmin)*random()
        L.append(np.array([x,y]))
        X.append(x)
        Y.append(y)
        for i in range(len(L)-1):
            if np.linalg.norm(L[i]-L[-1])<e:
                L.pop()
                X.pop()
                Y.pop()
    plt.plot([xmin,xmax,xmax,xmin,xmin],[xmin,xmin,xmax,xmax,xmin])    
    plt.scatter(X,Y,c="r",s=10)
    plt.axis("equal")
    plt.show()
    
    
def point_dans_triangle(point,triangle):        #Test si un point est dans un triangle ou pas, et renvoie True si c'est le cas
    p1,p2,p3=triangle
    xa,xb,xc=p1[0],p2[0],p3[0]
    ya,yb,yc=p1[1],p2[1],p3[1]
    x,y=point[0],point[1]
    s1=(x-xa)*(y-yb)-(y-ya)*(x-xb)
    s2=(x-xb)*(y-yc)-(y-yb)*(x-xc)
    s3=(x-xc)*(y-ya)-(y-yc)*(x-xa)
    plt.plot([xa,xb,xc,xa],[ya,yb,yc,ya])
    plt.scatter(x,y)
    plt.show()
    if s1*s2>0 and s2*s3>0:
        return(True)
    else:
        return(False)

def trouver_triangle(point,T,NP):       #Parcours le maillage T pour trouver dans quel triangle est le point, NP sont les points associés à leurs coordonnées
    for triangle in T:
        i1,i2,i3=triangle
        p1,p2,p3=NP[i1-1],NP[i2-1],NP[i3-1]
        if point_dans_triangle(point,[p1,p2,p3])==True:
            return(triangle)

def cercle(x0,y0,R):                    #Permet de tracer un cercle de centre (x0,y0) et de rayon R
    theta = np.linspace(0, 2*np.pi, 40)
    x = np.cos(theta)
    y = np.sin(theta)
    X=[x0+R*l for l in x]
    Y=[y0+R*l for l in y]
    plt.plot(X, Y)
    plt.axis("equal")
    
def cercle_circonscrit(T,NP):              #Permet de renvoyer le centre et le rayon du cercle circonscrit au triangle T
    p1,p2,p3=T
    x1,y1=NP[p1-1]
    x2,y2=NP[p2-1]
    x3,y3=NP[p3-1]
    A=np.array([[x2-x1,y2-y1],[x3-x1,y3-y1]])
    B=np.array([[(x2**2-x1**2+y2**2-y1**2)/2],[(x3**2-x1**2+y3**2-y1**2)/2]])
    X=np.linalg.solve(A,B)
    R=np.linalg.norm(X-np.array([[x1],[y1]]))
#    cercle(X[0],X[1],R)
#    plt.triplot([x1,x2,x3],[y1,y2,y3])
    return(X,R)

          
def est_dans_cercle(T1,point,nuage_point):           #Permet de savoir si pour un triangle et un point donné, le point est dans le cercle circonscrit au triangle
    p1,p2,p3=T1
    x1,y1=nuage_point[p1-1]
    x2,y2=nuage_point[p2-1]
    x3,y3=nuage_point[p3-1]
    A=np.array([[x2-x1,y2-y1],[x3-x1,y3-y1]])
    B=np.array([[(x2**2-x1**2+y2**2-y1**2)/2],[(x3**2-x1**2+y3**2-y1**2)/2]])
    X=np.linalg.solve(A,B)
    R=np.linalg.norm(X-np.array([[x1],[y1]]))
    Cx,Cy=X
#    cercle(Cx,Cy,R)
#    plt.plot([x1,x2,x3,x1],[y1,y2,y3,y1])
#    plt.scatter(Cx,Cy)
#    plt.scatter(point[0],point[1])
#    plt.show()
    D=np.linalg.norm(np.array([[point[0]],[point[1]]])-X)
    if D<R-10**(-6):
        return True
    else:
        return False
                 
def est_Delaunay(T1,T2,nuage_point):         #Pour deux triangles donnés, cette fonction renvoie si les deux triangles sont Delaunay
    t1,t2,t3=T1
    t4,t5,t6=T2
    p1,p2,p3=nuage_point[t1-1],nuage_point[t2-1],nuage_point[t3-1]
    p4,p5,p6=nuage_point[t4-1],nuage_point[t5-1],nuage_point[t6-1]
   
    T_1=T1[:]
    T_2=T2[:]
    
    for p in T1:
        if p in T2:
            T_1.remove(p)
    for p in T2:    
        if p in T1:
            T_2.remove(p)
    
    sommet1=T_1[0]
    sommet2=T_2[0]
    point1=nuage_point[sommet1-1]
    point2=nuage_point[sommet2-1]
    
    X1,R1=cercle_circonscrit([p1,p2,p3])
    X2,R2=cercle_circonscrit([p4,p5,p6])
    
    plt.triplot([p1[0],p2[0],p3[0],p1[0]],[p1[1],p2[1],p3[1],p1[1]])
    plt.triplot([p4[0],p5[0],p6[0],p4[0]],[p4[1],p5[1],p6[1],p4[1]])
    cercle(X1[0],X1[1],R1)
    cercle(X2[0],X2[1],R2)
   
    if est_dans_cercle(T1,point2,nuage_point)==True or est_dans_cercle(T2,point1,nuage_point)==True:
        return(False)
    else:
        return(True)
    
    
def voisin(maillage,t):                 #permet de trouver tous les voisins d'un triangle dans un maillage
    p1,p2,p3=t
    voisin=[]
    for triangle in maillage:
        if p1 in triangle and p2 in triangle and p3 not in triangle:
            voisin=voisin+[triangle]
        if p1 in triangle and p3 in triangle and p2 not in triangle:
            voisin=voisin+[triangle]
        if p2 in triangle and p3 in triangle and p1 not in triangle:
            voisin=voisin+[triangle]
    return(voisin)

def Delaunay_global(maillage,nuage_point):          #Vérifie si un maillage est Delaunay
    
    for triangle in maillage:
        voisins=voisin(maillage,triangle)
        for v in voisins:
            if est_Delaunay(v,triangle,nuage_point)==False:
                return(False)
    return(True)

def maillage_bis(maillage,nuage_point):     #Permet d'établir une liste de triangle avec leurs coordonnées (au lieux des points)
    n_maillage=[]
    for t in maillage:
        p1,p2,p3=t
        n_maillage=n_maillage+[[nuage_point[p1-1],nuage_point[p2-1],nuage_point[p3-1]]]
    return(n_maillage) 

def arete_dans_triangle(arete,triangle):
    A=set(arete)
    t1,t2,t3=triangle
    if A=={t1,t2} or A=={t2,t3} or A=={t1,t3}:
        return True
    else:
        return False

def bowyer_watson(maillage,nuage_point,point):      #Algorithme de Bowyer et Watson, en O(n) (et pas en O(n²) comme annoncé lors de la soutenance)
    Cavite=[]                                       # n nombre de points 
    N_maillage=[]
    nouveau_point=len(nuage_point)+1
    
    
    for t in maillage:
        if est_dans_cercle(t,point,nuage_point):
            Cavite=Cavite+[t]
    
    for t in Cavite:
        maillage.remove(t)
    
    for t in Cavite:
        t1,t2,t3=t
        Liste=Cavite[:]
        Liste.remove(t)
       
        for T in Liste:
           B=True
           if  arete_dans_triangle([t1,t2],T):
                B=False
                break
        if B:
            N_maillage=N_maillage+[[t1,t2,nouveau_point]]    
        
        
        for T in Liste: 
            B=True
            if  arete_dans_triangle([t2,t3],T):
                B=False
                break
            
        if B:
            N_maillage=N_maillage+[[t2,t3,nouveau_point]]
        
        for T in Liste:        
            B=True
            if arete_dans_triangle([t1,t3],T):
                B=False
                break
           
        if B:
            N_maillage=N_maillage+[[t1,t3,nouveau_point]]
                
        
    return(maillage+N_maillage,nuage_point+[point])    

def afficher_maillage(maillage,nuage_point):
    N=nuage_point
    for t in maillage:
        t1,t2,t3=t
        x1,y1=N[t1-1]
        x2,y2=N[t2-1]
        x3,y3=N[t3-1]
        plt.triplot([x1,x2,x3],[y1,y2,y3])
    plt.show()
    
def maillage(liste_point):                       #Algorithme de maillage d'un nuage de point en O(n²)
    M=[[1,2,4],[1,3,4],[2,3,4]]                  #Création du triangle 0, qu'on supprimera après 
    NP=[[-1,-1],[-1,10],[10,-1],liste_point[0]]   
    LP=liste_point[:]
    LP.pop(0)
    
    for P in LP:
        M,NP=bowyer_watson(M,NP,P)
    maillage=M[:]

    for L in M:
        if (1 in L) or (2 in L) or (3 in L):
            maillage.remove(L)

    return(maillage,NP)    
