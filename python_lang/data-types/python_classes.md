python – classes / objects

class Snake: 
  name="python"
  def change_name(self, new_name):
    self.name=new_name

snake = Snake()
print(snake.name)
snake1 = Snake()
print(snake1.name)
snake1.change_name("ralph")
print(snake1.name)


# // class is a template for creating objects - a way of organizing methods

class Dog: 
  def __init__(self, name):
    self.name = name
  def change_name(self, new_name): 
    self.name=new_name

mydog = Dog("charli")

print(mydog.name)
 

class Pup(Dog): 
  def __init__(self, name, size, age): #only place variables that will be passed in on runtime - so name comes from Dog -- I could add age, but then would have to pass it in when i create pup
    
    Dog.__init__(self, name)
    self.size=size
    self.age=age
  


now = Pup("Suz", "L", 4)
print(now.name)
    


https://www.youtube.com/watch?v=HDRxriLLFS0&list=PLAF3anQEEkzS-mjdX7s-D63bjLWRdhuFM&index=3

