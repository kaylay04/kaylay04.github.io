---
layout: project
type: project
image: img/Tree.jpg
title: "Hawaiian Dictionary"
date: 2024
published: true
labels:
  - Trees
  - Java
summary: "Implements a database of sayings in Hawaiian and English, with explanations in both languages. The database allows
insertion, lookup, and retrieval of sayings based on certain requirements. Use a balanced tree structure to maintain an ordered set of sayings.
Implementing functions for specific queries like finding sayings that contain particular words in either language."
---

This project focuses on designing and implementing a binary search tree (BST) to manage and search through Hawaiian and English sayings. By organizing the sayings in a BST, we can store the data efficiently and provide a way to retrieve them in sorted order or search by specific keywords with optimal performance. Below is an explanation of how the BST is structured, its functionalities, and the specific contribution to its development.

# Overview of the Project

The _BinarySearchTree_ class is at the core of this project. Each node in the tree stores a _Saying_ object, which contains a Hawaiian phrase and its English translation. Nodes are organized based on the Hawaiian text of the sayings, with smaller values placed in the left subtree and larger values in the right subtree. This ensures that the tree remains sorted, making it an efficient structure for both insertion and retrieval operations. 

The class includes several essential methods:
- _insert:_ This method inserts new sayings into the tree while maintaining the correct ordering. It uses a recursive helper function to determine the appropriate position for each new saying.
- _getAllSayings:_ This method retrieves all sayings from the tree in alphabetical order by performing an in-order traversal.
- _searchByWord:_ This method searches the tree for sayings that contain a specific word, either in their Hawaiian or English text, and returns a list of matches.

# Implementation Details
The private inner class _Node_ is used to encapsulate each tree node, containing a Saying object and references to the left and right child nodes. The _BinarySearchTree_ class itself manages the root node and provides public methods for interacting with the tree. Each operation leverages recursion to traverse the tree effectively, taking advantage of its inherent hierarchical structure.

Here is a deeper dive into the core functionality:
- Insertion: The _insert_ method allows for seamless addition of new sayings. When called, it delegates the work to a private recursive helper function that navigates the tree. Based on the comparison of Hawaiian text, the helper function determines whether the new saying should be placed in the left or right subtree. This ensures that the tree remains properly sorted and allows future operations to be carried out efficiently.
- Retrieving All Sayings: The _getAllSayings_ method uses an in-order traversal to retrieve sayings in alphabetical order by their Hawaiian text. This traversal visits the left subtree, processes the current node, and then visits the right subtree. As a result, the method compiles the sayings in sorted order, making it ideal for displaying all entries in a human-readable format.
- Search by Word: The _searchByWord_ method enables users to search for sayings containing a specific word. It performs a recursive traversal of the tree, checking each node’s Hawaiian and English text for matches. If a match is found, the saying is added to a results list. This feature is especially useful for finding relevant phrases based on partial input.

# Contribution to the Project
For this project I did the implementation of the _BinarySearchTree_ class which provides the foundation for storing and querying sayings. The recursive methods for insertion, traversal, and search demonstrate a deep understanding of BST operations and their application to real-world data management problems.

Additionally, the ability to search by both Hawaiian and English words ensures accessibility and practicality, allowing users to interact with the data intuitively. The combination of sorted retrieval and keyword-based search makes the BST a versatile and powerful data structure for this application.

# What I Learned From This

Working on this project taught me several important lessons, both technical and conceptual. First, I deepened my understanding of binary search trees (BSTs) and their practical applications in organizing and retrieving data efficiently. Implementing recursive methods for insertion and traversal helped me appreciate the elegant design of tree-based structures and the power of recursion in solving hierarchical problems.

I also learned how to apply sorting principles when structuring data, ensuring that the tree remained organized by the Hawaiian text. This reinforced the importance of maintaining order for fast and reliable operations like searching and in-order traversal.

Debugging and refining the code taught me the importance of attention to detail, such as correctly initializing lists and handling null nodes during traversal. These small but critical aspects underscored the importance of writing robust and error-free code in real-world applications.

Beyond the technical aspects, I gained insight into designing data structures to support user-friendly features. For example, allowing users to search sayings by either Hawaiian or English words showed me the importance of considering end-user needs during development.

Overall, this project strengthened my problem-solving skills, reinforced key programming concepts, and gave me a deeper appreciation for how data structures can make cultural content more accessible and meaningful.


Output: 
<img src="/img/HawaiianDictionaryOutput.jpg" alt="Output for Hawaiian Dictionary code." width="500"/>


    // Group: Justine Afaga, Blake Ilagan, Kayla Young
    /* Creating a class that holds the Hawaiian and English sayings, in addition to the definition: Representing a Hawaiian saying along with its English translations and explanations */

    public class Saying { 
    private String Hawaiian; 
    private String English; 
    private String hMeaning; 
    private String eMeaning; 
    }

     // Creating a constructor for initializing object
     public Saying(String Hawaiian, String English, String hMeaning, String eMeaning) {
        this.Hawaiian = Hawaiian;
        this.English = English;
        this.hMeaning = hMeaning;
        this.eMeaning = eMeaning;
    }

    // Getter method for Hawaiian saying 
    public String getHawaiian() { 
        return Hawaiian; 
    }

    // Getter method for English saying
    public String getEnglish() {
        return English; 
    }

    // Getter method for Hawaiian meaning 
    public String getHMeaning() {
        return hMeaning;
    }

    // Getter method for English meaning 
    public String getEMeaning() {
        return eMeaning; 
    }

    // toString to represent a Saying class object 
    public String toString() {
        return "Saying{" +
                "Hawaiian='" + Hawaiian + '\'' +
                ", English='" + English + '\'' +
                ", hMeaning='" + hMeaning + '\'' +
                ", eMeaning='" + eMeaning + '\'' +
                '}';
    }
    }

    // Balanced tree structure to maintain an ordered set of sayings:
    import java.util.ArrayList;
    import java.util.List;

    // Class representing a node in the binary search tree 
    class BinarySearchTree {
    private class Node {
        Saying saying;
        Node left, right;
        
        Node(Saying saying) {
            this.saying = saying;
        }
    }

    // Root of the binary search tree
    private Node root;

    // Method to insert a new saying recursively 
    public void insert(Saying saying) {
        root = insert(root, saying);
    }

    private Node insert(Node node, Saying saying) {
        if (node == null) {
            return new Node(saying);
        }
        if (saying.getHawaiian().compareTo(node.saying.getHawaiian()) < 0) {
            node.left = insert(node.left, saying);
        } else {
            node.right = insert(node.right, saying);
        }
        return node;
    }

    public boolean member(String hawaiian) {
        return member(root, hawaiian);
    }

    // Helper method to recursively check for the existence of a saying.
    private boolean member(Node node, String hawaiian) {
        if (node == null) {
            return false;
        }
        int cmp = hawaiian.compareTo(node.saying.getHawaiian());
        if (cmp == 0) {
            return true;
        } else if (cmp < 0) {
            return member(node.left, hawaiian);
        } else {
            return member(node.right, hawaiian);
        }
    }

    // Returns a list of all sayings in the binary search tree in alphabetical order 
    public List<Saying> getAllSayings() {    
        List<Saying> sayings = new ArrayList<>();
        inOrderTraversal(root, sayings);
        return sayings;
    }
    
    // Method to perform in-order traversal of the binary search tree 
    private void inOrderTraversal(Node node, List<Saying> sayings) {
        if (node == null) {
            return;
        }
        inOrderTraversal(node.left, sayings);
        sayings.add(node.saying);
        inOrderTraversal(node.right, sayings);
    }

    // Search through the binary search tree if it has a specific word in either Hawaiian or English 
    public List<Saying> searchByWord(String word) {
        List<Saying> sayings = new ArrayList<>();
        searchByWord(root, word, sayings);
        return sayings;
    }

    // Method to recursively search for sayings by word 
    private void searchByWord(Node node, String word, List<Saying> sayings) {
        if (node == null) {
            return;
        }
        searchByWord(node.left, word, sayings);
        if (node.saying.getHawaiian().contains(word) || node.saying.getEnglish().contains(word)) {
            sayings.add(node.saying);
        }
        searchByWord(node.right, word, sayings);
    }
    }

    // Implementing query functions:

    import java.util.HashMap; 
    import java.util.List; 
    import java.util.Map; 

    // Database of sayings using a binary search tree 
    public class SayingDatabase {
    // Binary search tree for storing the sayings 
    private BinarySearchTree tree = new BinarySearchTree();

    // Index for Hawaiian sayings 
    private Map<String, List<Saying>> hawaiianIndex = new HashMap<>();

    // Index for English sayings 
    private Map<String, List<Saying>> englishIndex = new HashMap<>();

    // Inserting a saying into the database and updating the indices 
    public void insert(Saying saying) {
        tree.insert(saying);
        indexSaying(saying);
    }

    // Checks if a saying exists in the database
    public boolean member(String hawaiian) {
        return tree.member(hawaiian);
    }

    // Indexes the saying for quick search by word 
    private void indexSaying(Saying saying) {
        String[] hawaiianWords = saying.getHawaiian().split("\\s+");
        // Adds each word to the Hawaiian index map
        for (String word : hawaiianWords) {
            hawaiianIndex.computeIfAbsent(word, k -> tree.searchByWord(word));
        }
        // Indexes by English words and translation into individual words 
        String[] englishWords = saying.getEnglish().split("\\s+");
        // Adds each word to the English index map
        for (String word : englishWords) {
            englishIndex.computeIfAbsent(word, k -> tree.searchByWord(word));
        }
    }

    // Returns a list of sayings containing the specified Hawaiian word 
    public List<Saying> meHua(String word) {
        return hawaiianIndex.getOrDefault(word, List.of());
    }

    // Returns a list of sayings containing the specified English word 
    public List<Saying> withWord(String word) {
        return englishIndex.getOrDefault(word, List.of());
    }

    // Returns all sayings in the database in alphabetical order 
    public List<Saying> getAllSayings() {
        return tree.getAllSayings();
    }
    }

    // Printing and testing out the functionality 

    public class Main {
        public static void main(String[] args) {
            SayingDatabase database = new SayingDatabase();
            // Sample sayings
            Saying saying1 = new Saying("Aia i ka huki ʻulua", "There is the fishing of the ulua", "Explanation in Hawaiian", "Explanation in English");
            Saying saying2 = new Saying("Hiki i ke kanaka", "It can be done by a person", "Explanation in Hawaiian", "Explanation in English");

        // Insert sayings into the database
        database.insert(saying1);
        database.insert(saying2);

        // Print all sayings
        System.out.println("All Sayings:");
        for (Saying saying : database.getAllSayings()) {
            System.out.println(saying);
        }

        // Print sayings containing the word "huki" in Hawaiian
        System.out.println("\nSayings containing 'huki' (in Hawaiian):");
        for (Saying saying : database.meHua("huki")) {
            System.out.println(saying);
        }

        // Print sayings containing the word "fishing" in English
        System.out.println("\nSayings containing 'fishing' (in English):");
        for (Saying saying : database.withWord("fishing")) {
            System.out.println(saying);
        }
    }
    }

