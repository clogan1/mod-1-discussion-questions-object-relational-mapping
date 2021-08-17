# ORM Discussion Questions

Consider the following questions with the people at your table. Write down your answers in a notebook or on a whiteboard. 

1. First, discuss with your table - what is an ORM? Why is an ORM useful?

    ORM = Object Relational Mapping
    Middleman between Ruby objects and a database; how you get the data in the right format to pass it between the two
    
2. Pretend that you're building Twitter. Let's say that a tweet has a message and belongs to a User. A User has a username and has_many tweets. What columns would be on those two tables?

  User Table: id, username ...
  Tweets Table: id, tweet, user_id (foreign key that = user's id)

3. Now that we have our tables, pretend that we are defining a method on our User class that returns all the tweets. What SQL fires when this method is called?
  
  #all tweets ever
  SELECT * FROM tweets
  
  #all tweets from a particular user
  SELECT * FROM tweets WHERE user_id = X
  #user_id = self.id
  
4. Writing out all of these database interactions by hand can be messy. How would you create a method on the superclass to make sure the correct SQL fires for each class?

```
class LiveRecord

  def self.all 
    sql = <<-SQL
    SELECT *
    FROM ?
    SQL
    
    DB[:conn].execute(sql, table)
  end
end

class Dog < LiveRecord
end

class Cat < LiveRecord

end

Dog.all #=> 'SELECT * FROM dogs'
Cat.all #=> 'SELECT * FROM cats'
```


