#pythonRep
#for keeping genuine code - having solutions for small / utility features or services

#05th Feb. 2020
#Python program to automatically generate CAPTCHA and 
#verify user provided value to check if the user is a human or a bot
#by Chandra Karri during Feb. 2020

#for random number generation
import random
#for using reduce function
import functools

#Returns true if given two lists are same 
def checkCaptcha(captcha, user_captcha):
  #sort the lists of characters or numerics before comparing
	captcha.sort()
	user_captcha.sort()
	return functools.reduce(lambda i, j : i and j, map(lambda m, k: m == k, captcha, user_captcha), True)
 

#Generates a CAPTCHA of given length 
def generateCaptcha(n): 
 
  #Characters to be included 
	fixed_set = tuple('abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789')
	chars = [i for i in fixed_set ]
	
  #Generate n characters from above set and add these characters to captcha. 
	captcha = []
	while(n):
		captcha.append(chars[random.randint(0, 100)%62])
		n -= 1
	return captcha


#Invocation, generation, comparision code in main method 
def main():

  #Generate a random CAPTCHA
	str1 = ""
	captcha = generateCaptcha(5)
	for ele in captcha:
		str1 += ele
	print("Generated captcha is " + str1 )

  #Ask user to enter a CAPTCHA 
	usr_captcha = None 
	usr_captcha_entered = str(input("Enter the captcha \n"))
	usr_captcha = [i for i in usr_captcha_entered] 

  #Notify user about matching status 
	if (checkCaptcha(captcha, usr_captcha)): 
		print("\nCAPTCHA Matched") 
	else:
		print("\nCAPTCHA Not Matched")

main()
