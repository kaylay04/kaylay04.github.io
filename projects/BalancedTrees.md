---
layout: project
type: project
image: img/Tree.jpg
title: "Balanced Trees"
date: 2024
published: true
labels:
  - Trees
  - Java
summary: "Implements a database of sayings in Hawaiian and English, with explanations in both languages. The database allows
insertion, lookup, and retrieval of sayings based on certain requirements. Use a balanced tree structure to maintain an ordered set of sayings.
Implementing functions for specific queries like finding sayings that contain particular words in either language."
---
// Group: Justine Afaga, Blake Ilagan, Kayla Young
// Creating a class that holds the Hawaiian and English sayings, in addition to the definition: 
/* Representing a Hawaiian saying along with its English translations and explanations */

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

class BinarySearchTree {
    // Class representing a node in the binary search tree 
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
'''

