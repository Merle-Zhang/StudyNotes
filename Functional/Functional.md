# Functional Programming

* Evaluation

  * Normal evaluation = lazy evaluation
  * Applicative evaluation = eager evaluation
  * Normal evaluation is an evaluation strategy that **may** terminate when applicative evaluation does not.

* `foldr (-) 4 [3,2,1]` = `3-(2-(1-4))`

* `$`

  ```hs
  ($) :: (a -> b) -> a -> b
  
  putStrLn (show $ 1 + 1)
  putStrLn $ show (1 + 1)
  putStrLn $ show $ 1 + 1
  ```

* `$` vs `.`
  * The `$` operator is for avoiding parentheses.  Anything appearing after it will take precedence over anything that comes before.
  * The primary purpose of the `.` operator is not to avoid  parentheses, but to chain functions. It lets you tie the output of  whatever appears on the right to the input of whatever appears on the  left.  This usually also results in fewer parentheses, but works  differently.
  ```hs
  putStrLn (show (1 + 1))
  
  (putStrLn . show) (1 + 1)
  
  putStrLn . show $ 1 + 1
  ```

* List Comprehension Order

  ```haskell
  [(x,y) | x <- [1..10000], y <- [1..100], x==2000, odd y]
  [(x,y) | x <- [1..10000], x==2000, y <- [1..100], odd y]
  ```

* ```haskell
  [(x,y) | x <- [1..10000], y <- [1..100], x==2000, odd y]
      
  for x in [1..10000]:
      for y in [1..100];
          if x == 2000:
              if odd y:
                  yield (x,y)
                      
  [(x,y) | x <- [1..10000], x==2000, y <- [1..100], odd y]
      
  for x in [1..10000]:
      if x == 2000;
          for y in [1..100]:
              if odd y:
                  yield (x,y)
  ```

* `data` vs `newtype` vs `type`

  * `data`: zero or more constructors, each can contain zero or more values.
  * `newtype`: similar to above but exactly one constructor and one value in that  constructor, and has the exact same runtime representation as the value  that it stores.
  * `type`: type synonym, compiler more or less forgets about it once it is expanded.

* `div` vs `/`

  ```hs
  > :t div
  div :: Integral a => a -> a -> a
  > :t (/)
  (/) :: Fractional a => a -> a -> a
  > 3 / 5
  0.6
  > 3 `div` 5
  0
  > (-3) `div` 5
  -1
  > (-3) `quot` 5
  0
  > [x `mod` 3 | x <- [-10..10]]
  [2,0,1,2,0,1,2,0,1,2,0,1,2,0,1,2,0,1,2,0,1]
  > [x `rem` 3 | x <- [-10..10]]
  [-1,0,-2,-1,0,-2,-1,0,-2,-1,0,1,2,0,1,2,0,1,2,0,1]
  ```

* ```haskell
  (++) :: [a] -> [a] -> [a]
  xs ++ ys = foldr (:) ys xs
  ```

* `(\x->x/='\n')` is equivelent to `(/='\n')`

  * Just add or remove `\x->x`

* Monad

  * List Comprehension

    ```hs
    [x*2 | x<-[1..10], odd x]
    
    do
       x <- [1..10]
       guard (odd x)
       return (x * 2)
       
    [1..10] >>= (\x -> guard (odd x) >> return (x*2))
    ```

  * ``` haskell
    class Monad m where
    	(>>) :: m a -> m b -> m b
    	(>>=) :: m a -> (a -> m b) -> m b
    	return :: a -> m a
    	
    	
    	
    	
    do {e}						--> e
    do {e; statments}			--> e >> do {stmts}
    do {x <- e; statements}		--> e >>= (\x -> do {stmts})
    do {let x = e; statememts}	--> do {stmts} where x = e
    
    return :: a -> Maybe a
    return x = Just x
    
    (>>=) :: Maybe a -> (a -> Maybe b) -> Maybe b
    Nothing >>= _ = Nothing
    Just x  >>= k = k x
    
    (>>) :: Maybe a -> Maybe b -> Maybe b
    Nothing >> _ = Nothing
    Just _ >> mb = mb
    ```

  * A valid instance of the Monad typeclass should satisfy:

    * Left Unit Law: `return x >>= f` $=$ `f x`
    * Right Unit Law: `mx >>= return` $=$ `mx`
    * Associative Law: `(mx >>= f) >>= g` $=$ `mx >>= (\x -> f x >>= g)`

* Instructions vs Functions

  * **Functions (pure)** always give the same result for the same arguments
  * **Instructions (impure)** can behave differently on different occasions

* Sampling

  ```haskell
  class Arbitrary a where
  	arbitrary :: Gen a
  
  sample :: Gen a -> IO a
  
  sample (arbitraty :: Gen Bool)
  // True False True True
  sample (arbitrary :: Gen Int)
  // 1 0 -5 23 435
  sample (return True)
  // True True True
  sample (doTwice (arbitrary :: Gen Integer))
  // (12, -6) (5, 3) (3, 2)
  
  evenInteger :: Gen Integer
  evenInteger = do n <- arbitrary
  			  return (2*n)	
  sample evenInteger
  // -32 -6 0 4 6
  
  // Library functions
  // choose :: Random a => (a,a) => Gen a
  sample (choose (1,10) :: Gen Integer)
  // 6 7 3 10 4
  
  // oneof :: [Gen a] -> Gen a
  sample (oneof [return 1, return 10])
  // 1 1 10 1 10
  
  data Suit = Spades | Hearts | Dismonds | Clubs
  suit :: Gen Suit
  suit = oneof [return Spades,
  			  return Hearts,
  			  return Diamonds,
  			  return Clubs]
  sample suit
  // Spades Hearts Diamonds Clubs
  
  data Rank = Numeric Integer | Jack | Queen | King | Ace
  rank :: Gen Rank
  rank = oneof [return Jack,
  			  return Queen,
  			  return King,
  			  return Ace,
  			  do r <- choose (2,10)
  			  	 return (Numeric r)]
  sample rank
  // Queen King (Numeric 4) (Numeric 3)
  			  	 
  data Card = Card Rank Suit
  card :: Gen Card
  card = do r <- rank
  		  s <- suit
  		  return (Card r s)
  sample card
  // (Card Ace Hearts) (Card King Diamonds) (Card Queens Clubs)
  
  data Hand = Empty | Add Card Hand
  hand :: Gen Hand
  hand = oneof [return Empty,
  			  do c <- card
  			  	 h <- hand
  			  	 return (Add c h)]
  sample hand
  // Empty, Add (Card Queen Diamonds) Empty, ...
  
  instance Arbitrary Suit where
  	arbitrary = suit
  	
  // tast case distribution
  prop_rank r = collect r (valirRank r)
  	where validRank (Numeric r) = 2 <= r && r <= 10
  		  validRank _ 			= True
  // face card occur much more frequentl then numeric cards
  
  // Fixing the Generator
  // frequency :: [(Int, Gen a)] => Gen a
  rank :: Gen Rank
  suit = frequency [(1,return Jack),
  				  (1,return Queen),
  				  (1,return King),
  				  (1,return Ace),
  				  (9, do r <- choose (2,10)
  				  		 return (Numeric r))]
  prop_hand h = collect (size h) True
  // 53% 0, 25% 1, 9% 2...
  
  // fixing
  hand = frequency [(1,return Empty),
  				  (4, do c <- card
  				  		 h <- hand
  				  		 return (Some c h))]
  // 22% 0, 13% 2, 13% 1...				  		 
  ```

* Type class

  ```haskell
  class Show a where
  	show :: a -> String
  
  show :: Show a => a -> String
  
  instance Show Bool where
  	show True = "True"
  	show False = "False"
  	
  // multiple derives
  	...
  	deriving (Show, Eq)
  	
  // hierarchy	
  class Eq a => Ord a where
  
  doTwice :: Monad m => m a -> m (a,a) // data IO a...
  ```

* I/O

  * ```haskell
    do  
        foo <- putStrLn "Hello, what's your name?"  
        name <- getLine  
        putStrLn ("Hey " ++ name ++ ", you rock!") 
    ```

  * ```haskell
    import Data.Char  
    
    main = do  
        putStrLn "What's your first name?"  
        firstName <- getLine  
        putStrLn "What's your last name?"  
        lastName <- getLine  
        let bigFirstName = map toUpper firstName  
        	bigLastName = map toUpper lastName  
        putStrLn $ "hey " ++ bigFirstName ++ " " ++ bigLastName ++ ", how are you?"  
    ```

  * ```haskell
    main = do  
    	a <- return "hell"  
    	b <- return "yeah!"  
    	putStrLn $ a ++ " " ++ b  
    ```

    So you see, return is sort of the opposite to <-. While return takes a value and wraps it up in a box, <- takes a box (and performs it) and takes the value out of it, binding it to a name. But doing this is kind of redundant, especially since you  can use *let* bindings in *do* blocks to bind to names, like so: 

    ```haskell
    main = do  
    	let a = "hell"  
    		b = "yeah"  
    	putStrLn $ a ++ " " ++ b  
    ```

    

