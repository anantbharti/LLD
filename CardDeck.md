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
