Design the data structures for a generic deck of cards.

Suite.java
```java
public enum Suite
{
    Club,
    Diamond,
    Heart,
    Spade
}
```
CardI.java
```java
public interface CardI {
	Suite getSuit();
    int getNumber();
}
```
Card.java
```java
public class Card implements CardI
{
    private int number;
    private Suite suite;
    
    public Card(Suite suite,int number)
    {
        this.suite = suite;
        this.number = number;
    }
    
    public Suite getSuit()
    {
        return this.suite;
    }
    
    public int getNumber()
    {
        return this.number;
    }
    
}
```
CardDeck.java
```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class CardDeck
{
    List<Card> cards;
    
    public CardDeck()
    {
        cards = new ArrayList<Card>();
        
        for(Suite s: Suite.values())
        {
            for(int i=1;i<=13;i++)
            {
                Card card = new Card(s,i);
                cards.add(card);
            }
        }
    }
    
    public void shuffle()
    {
    	Collections.shuffle(cards);
    }
    
    public void showCards()
    {
        for(int i=0;i<52;i++)
        {
        	System.out.println(i+1 + " " + cards.get(i).getSuit() + " " + cards.get(i).getNumber());
        }
    }
}
```
Main.java
```java
public class Main {

	public static void main(String[] args) {
		
		CardDeck cardDeck = new CardDeck();
		cardDeck.showCards();
		cardDeck.shuffle();
		cardDeck.showCards();
	}

}
```

Output
```
1 Club 1
2 Club 2
3 Club 3
4 Club 4
5 Club 5
6 Club 6
7 Club 7
8 Club 8
9 Club 9
10 Club 10
11 Club 11
12 Club 12
13 Club 13
14 Diamond 1
15 Diamond 2
16 Diamond 3
17 Diamond 4
18 Diamond 5
19 Diamond 6
20 Diamond 7
21 Diamond 8
22 Diamond 9
23 Diamond 10
24 Diamond 11
25 Diamond 12
26 Diamond 13
27 Heart 1
28 Heart 2
29 Heart 3
30 Heart 4
31 Heart 5
32 Heart 6
33 Heart 7
34 Heart 8
35 Heart 9
36 Heart 10
37 Heart 11
38 Heart 12
39 Heart 13
40 Spade 1
41 Spade 2
42 Spade 3
43 Spade 4
44 Spade 5
45 Spade 6
46 Spade 7
47 Spade 8
48 Spade 9
49 Spade 10
50 Spade 11
51 Spade 12
52 Spade 13
1 Spade 12
2 Club 2
3 Club 6
4 Spade 1
5 Spade 13
6 Club 1
7 Spade 4
8 Heart 5
9 Club 9
10 Diamond 4
11 Diamond 5
12 Club 12
13 Diamond 13
14 Heart 12
15 Spade 11
16 Heart 3
17 Diamond 7
18 Spade 7
19 Club 8
20 Heart 10
21 Heart 9
22 Spade 2
23 Heart 6
24 Spade 3
25 Diamond 6
26 Diamond 3
27 Club 5
28 Spade 5
29 Spade 8
30 Diamond 8
31 Spade 6
32 Heart 11
33 Club 4
34 Heart 7
35 Diamond 9
36 Diamond 1
37 Heart 8
38 Club 7
39 Diamond 11
40 Club 11
41 Club 10
42 Heart 4
43 Diamond 12
44 Diamond 10
45 Heart 1
46 Heart 2
47 Club 3
48 Club 13
49 Spade 9
50 Heart 13
51 Diamond 2
52 Spade 10
```
