# Menu
import java.util.*;   
	public class Menu {
            public static void main(String[] args){
                Scanner kbd = new Scanner(System.in);
                Catalog store = new Catalog(3);
                int itemnum;
                Item item;

                

                try {
                    store.insert
                      (new Music(1111, "Gold", 12.00, "Abba"));
                    store.insert
                      (new Movie(2222, "Mamma Mia", 16.00, "Meryl Streep"));
                    store.insert
                      (new Book(3333, "DaVinci Code", 8.00, "Dan Brown"));
                    store.insert
                      (new Music(4444, "Legend", 15.00, "Bob Marley"));
                } catch (CatalogFull exc) {
                    System.out.println(exc);
                }
                 Scanner scan = new Scanner(System.in);
                 System.out.println( "Item number (0 to quit)?  ");
                 itemnum = scan.nextInt();
                
                 while(itemnum!=0){
                    try {
                        item= store.find(itemnum);
                        if (itemnum != 0){
                         System.out.println(item);   
                        }
                    }catch(ItemNotFound exc2){                    
                    System.out.println(exc2);
                }
                 System.out.printf("%n");
                 System.out.println( "Item number (0 to quit)?  ");
                 itemnum = scan.nextInt();
                }

        }
    }   
    
######################################################
        public class Item {
            private int itemnum;
            private String title;
            private double price;

            // Construct a new item object.
            public Item(int id, String t, double p) {
                itemnum = id;
                title = t;
                price = p;
            }

            // Return the item number of this item.
            public int getItemNumber() {
                return itemnum;
            }

            // Return the item type. This is overridden in subclasses.
            public String getItemType() {
                return "Item";
            }

            // Return a printable String represenation of this item.
            public String toString() {
                String line1, line2, line3, line4, out;
                String itemtype = this.getItemType();
                line1 = String.format("Item number: %d%n", itemnum);
                line2 = String.format("Item type:   %s%n", itemtype);
                line3 = String.format("Item title:  %s%n", title);
                line4 = String.format("Item price:  %.2f%n", price);
                out = line1 + line2 + line3 + line4;
                return out;
            }
        }
    
#############################################################################
        // This exception is thrown when searching for an item
        // that is not in the catalog.
        public class ItemNotFound extends Exception {
            public ItemNotFound(int id) {
                super(String.format("Item %d was not found.", id));
            }
        }
######################################################################################
        public class Catalog {
            private Item[] list;
            private int size;

            // Construct an empty catalog with the specified capacity.
            public Catalog(int max) {
                list = new Item[max];
                size = 0;
            }

            // Insert a new item into the catalog.
            // Throw a CatalogFull exception if the catalog is full.
            public void insert(Item obj) throws CatalogFull {
                if (list.length == size) {
                    throw new CatalogFull();
                }
                list[size] = obj;
                ++size;
            }

            // Search the catalog for the item whose item number
            // is the parameter id.  Return the matching object 
            // if the search succeeds.  Throw an ItemNotFound
            // exception if the search fails.
            public Item find(int id) throws ItemNotFound {
                // Write your code here.
                for(int dumb=0;dumb<size;++dumb){
                    if (id== list[dumb].getItemNumber()){
                        return list[dumb];   

                    }
            }
            throw new ItemNotFound(id);
        }
    }
#############################################################################
        // This exception is thrown when trying to insert an item
        // when the catalog is full.
        public class CatalogFull extends Exception {
            public CatalogFull() {
                super("The catalog is full.");
            }
        }
#############################################################################
        public class Music extends Item {
            private String artist;

            // Construct a new book object.
            public Music(int id, String t, double p, String a) {
                super(id, t, p);
                artist = a;
            }

            // Return the item type. Overrides method from class Item.
            public String getItemType() {
                return "Music";
            }

            // Return a printable String representation of this item.
            // Overrides method from class Item.
            public String toString() {
                String part1, part2, out;
                part1 = super.toString();
                part2 = String.format("artist:      %s%n", artist);
                out = part1 + part2;
                return out;
            }
        }
###############################################################################
        public class Movie extends Item {
            private String star;

            // Construct a new book object.
            public Movie(int id, String t, double p, String a) {
                super(id, t, p);
                star = a;
            }

            // Return the item type. Overrides method from class Item.
            public String getItemType() {
                return "Movie";
            }

            // Return a printable String representation of this item.
            // Overrides method from class Item.
            public String toString() {
                String part1, part2, out;
                part1 = super.toString();
                part2 = String.format("Star:      %s%n", star);
                out = part1 + part2;
                return out;
            }
        }
####################################################################################
        public class Book extends Item {
            private String author;

            // Construct a new book object.
            public Book(int id, String t, double p, String a) {
                super(id, t, p);
                author = a;
            }

            // Return the item type. Overrides method from class Item.
            public String getItemType() {
                return "Book";
            }

            // Return a printable String representation of this item.
            // Overrides method from class Item.
            public String toString() {
                String part1, part2, out;
                part1 = super.toString();
                part2 = String.format("Author:      %s%n", author);
                out = part1 + part2;
                return out;
            }
        }
##############################################################################################        

