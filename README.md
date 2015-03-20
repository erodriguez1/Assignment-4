# Assignment-4
Heat Capacity of a Solid and Numerical Integral 


# Elizabeth Rodriguez
# Physics 50733
# Assignment 4


# 1: Heat Capacity of a solid
# Debyes theory of solids gives that heat capacity of a solid at 
#temperature T to be:
# Cv = 9VPK(T/sigma)^3* integral from 0-sigma/T (x^4*e^x)/((e^x-1)^2)dx
#where V is the volume of the solid, P is the number density of atoms, K
#is the Boltzmann constant, sigma is the so-called Debye temperature, a 
#property of solids that depends on their density and speed of sound.
# For full credit: Email your program plus the plotted output that shows
#heat capacity as a function of temperature


# A) Write a python function Cv(T) that calculates Cv for a given value
#of the temperature, for a sample consisting of 1000 cubic centimeters of
#solid aluminum, which has a number density of P= 6.022X10^28 m^-3 and a 
#Debye temperature of sigma= 428K. Use the trapezoial rule to evaluate the
#integral with N= 1000 sample points. Hint: The value of the integrand at
#x = 0 is zero.

# Standard function
from math import exp
from operator import truediv # Standard division did not work nor calling _future_ because it did not exist
from numpy import arange # Range

def f(x):
    return truediv(((x**4)*(exp(x))),((exp(x)-1)**2))  # Inside the integral
    
N = 1000.0 # Sample points
a = 1.0 # Starting point
T = int(input('Enter temperature you wished to integrate with:'))
V = 0.001 # Volume of solid
p = 6.022**28 # Number density
O = 428 # Debye temperature
k = 1.3806488**-23 # Boltzmann constant
b = truediv(O,T) # Ending point
h = truediv((b-a),N)

s = 0.50*f(a) + 0.50*f(b) #Trapezoidal Rule
for i in arange(N):
    s += 9*V*p*k*((truediv(T,O))**3)*f(a+i*h) # What you are computing
print(h*s) 

# B) Use your function to make a graph of the heat capacity as a function
#of temperature from T= 5K to T= 500K.    
# Note: That there is no known way to perform this particular integral
#analytically, so numerical approaches are the only way forward.
# For full credit: Email your program plus the plotted output that shows
#E(x) as a function of x.

from math import exp
from operator import truediv # Standard division did not work nor calling _future_ because it did not exist
from numpy import arange # Range
from pylab import plot, title, xlabel, ylabel, show

def f(x):
    return truediv(((x**4)*(exp(x))),((exp(x)-1)**2))  # Inside the integral
    
N = 1000.0 # Sample points
a = 1.0 # Starting point, did not want to compute when equaled to zero
T_1 = int(input('Enter first temperature you wished to integrate with:')) # Input 5K
T_2 = int(input('Enter second temperature you wished to integrate with:')) # Input 500K
V = 0.001 # Volume of solid
p = 6.022**28 # Number density
O = 428 # Debye temperature
k = 1.3806488**-23 # Boltzmann constant
b_1 = truediv(O,T_1) # Ending point 1
b_2 = truediv(O,T_2) # Ending point 2
h_1 = truediv((b_1-a),N)
h_2 = truediv((b_2-a),N)


#Trapezoidal Rule
s_1 = 0.50*f(a) + 0.50*f(b_1) 
s_2 = 0.50*f(a) + 0.50*f(b_2)
for i in arange(0, N):
    y_1 = f(a+i*h_1)
    y_2 = f(a+i*h_2)
    s_1 += 9*V*p*k*((truediv(T_1,O))**3)*y_1 # What you are computing
    s_2 += 9*V*p*k*((truediv(T_2,O))**3)*y_2
print'When temperature equaled (K):', T_1, 'The resulting integral is:','{:.3e}'.format(float(h_1*s_1)) 
print'When temperature equaled (K):', T_2, 'The resulting integral is:','{:.3e}'.format(float(h_2*s_2))

plot( T_1, s_1, 'bo', T_2, s_2, 'ro')
title('E(x) as a function of x')
xlabel('x')
ylabel('E(x)')
show()

# 2: Numerical Integral
# Consider the integral:
# E(x)= integral from 0-x e^(x^2)dx


# A) Write a program to calculate E(x) for values of x from 0 to 3 in 
#steps of 0.1. Choose for yourself what method you will use for performing
#the integral and a suitable number of slices.

from math import exp
from operator import truediv
from numpy import arange
from pylab import plot, title, xlabel, ylabel, show

def f(x):
    return exp(x**2)
    
a = 0.0
b = 3.0
N = 0.1
h = truediv((b-a),N)


s = 0.5*f(a) + 0.5*f(b)
for i in arange(N):
    s += f(a+i*h)
    
print(h*s)

# B) When you are convinced your program is working, extend it further to
#make a graph of E(x) as a function of x. 

plot( h, s, 'bo')
title('E(x) as a function of x')
xlabel('x')
ylabel('E(x)')
show()
