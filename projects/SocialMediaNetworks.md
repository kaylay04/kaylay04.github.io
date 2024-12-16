---
layout: project
type: project
image: img/SocialMediaNetwork.jpg
title: "Social Media Networks"
date: 2024
published: true
labels:
  - Graphs
  - Algorithms
  - Python
summary: "This code initializes a graph to represent users and their posts, adding nodes for users and posts and creating edges for relationships like authorship, comments, and views. It includes functions to identify and highlight the top 10 important posts, interesting users, and trending posts based on comments and views. Additionally, it adds edges for quoted or referred posts. This code also displays the results, showing the important posts, interesting users, and trending posts."
---

This project focuses on designing and implementing a graph to model the structure and interactions within a social media platform. The graph representation helps capture the relationships between users and posts, making it easier to analyze user activity, post popularity, and interactions between content. By organizing data into a graph structure, we can efficiently retrieve information such as important posts, interesting users, and interactions between content. The graph consists of nodes, representing users and posts, and edges, representing relationships such as authored posts, comments, and views.

# Overview of the Project

The core structure of this project is a graph, where nodes represent users and posts, and edges represent interactions such as authored posts, comments, and views. Each user has their own profile, including attributes like age, gender, region, and a list of posts, comments, and views. Posts, on the other hand, have a unique _post_id_ and contain content along with information on who commented on or viewed them. This project models the interactions in the social media space, including user engagement and content influence.

# Implementation Details 

The graph is structured as an object containing two primary components: _nodes_ and _edges_. The _nodes_ object is a dictionary where each key is a node ID (either a user or post), and the value is an object containing information about the node's attributes. The _edges_ list stores relationships between nodes in the form of objects that define the direction (from one node to another) and the type of relationship (e.g., _authored_, _commented_, _viewed_, _quotes_, or _referred_). This structure allows the graph to represent complex relationships and interactions between users and posts.

# Core Functionalities

There are several core functions designed to handle the graph operations. The _addNode_ function is used to add nodes for both users and posts. Each user’s node contains information such as their name, age, gender, and location, along with a list of their posts, comments, and views. Each post node stores the content, comments, views, and its relationships with other posts. The _addEdge_ function creates edges between users and posts (for authorship), between users and other users' posts (for comments and views), and between posts that reference or quote other posts.

Additionally, the _getImportantPosts_ function retrieves posts based on a sorting criterion, such as views or comments, to help identify the most influential posts in the network. The _getInterestingUsers_ function finds interesting users based on their engagement level, such as the total number of comments or views across their posts. Lastly, the _addQuotedReferredEdges_ function handles posts that quote or refer to other posts, creating additional connections between content and allowing users to trace the influence of one post on another. 

# Contribution to the Project

For this project, I was responsible for implementing the core graph structure and the methods for managing the nodes and edges. I designed and developed the functions for adding nodes, representing users and posts, and creating edges to define relationships such as authorship, comments, and views. Additionally, I implemented the functionality to handle quoted and referred posts, which adds a layer of complexity to the graph and allows for a more connected content network. These contributions helped to ensure the graph accurately represented user interactions and post dynamics.

# What I Learned From This

Working on this project taught me several key lessons related to graph theory, data structures, and user interaction modeling. First, I deepened my understanding of graphs and how they can be used to model real-world social networks. Creating and managing relationships between users and posts highlighted the power of graphs in representing complex interactions in a way that is easy to manipulate and analyze. I also gained a deeper appreciation for sorting and filtering data in a meaningful way. For example, retrieving the most popular posts or the most engaged users through sorting allowed me to understand how data structures can be used to provide meaningful insights and recommendations.

Additionally, I improved my skills in working with recursive methods and traversing graphs effectively. Implementing features like searching for quotes and references required me to explore how posts and users can be connected in multiple ways, leading to a richer representation of social media dynamics. Overall, this project enhanced my understanding of graph-based data structures and their applications in analyzing social media data, while also honing my ability to design and implement scalable, efficient algorithms for real-world data management problems.

Output: 
<img src="/img/SocialMediaNetworksOutput.jpg" alt="Output for Social Media Networks code." width="auto" height="auto"/>

    Justine Afaga
    Alexis Karl Buted
    Kayla Young


    from wordcloud import WordCloud
    import matplotlib.pyplot as plt

    /* This code initializes a dictionary called `social_media_data` to represent social media users and their associated data.  It contains two users, each with a list of posts, comments, views, and personal attributes (age, gender, region). The posts are stored with unique `post_id`s, along with their content, number of comments, and views.*/

    social_media_data = {
        "users": {
            "user1": {
                "posts": [
                    {"post_id": 1, "content": "Hello world! Welcome to the social media world.", "comments": 5, "views": 100},
                    {"post_id": 2, "content": "My second post. Enjoy your day!", "comments": 2, "views": 50},
                ],
                "comments": [1, 2],
                "views": [1, 2],
                "attributes": {"age": 25, "gender": "female", "region": "North America"}
            },
            "user2": {
                "posts": [
                    {"post_id": 3, "content": "User2's post. This is a sample post.", "comments": 10, "views": 200}
                ],
                "comments": [3],
                "views": [3],
                "attributes": {"age": 30, "gender": "male", "region": "Europe"}
            }
        }
    }

    /* This code initializes an empty graph structure using a dictionary named `graph`. The `nodes` key holds a dictionary meant to store individual nodes, like users and posts, along with their attributes. The `edges` key holds a list that will store the edges between these nodes, representing relationships like authorship, commenting, or viewing. */

    graph = {
        "nodes": {},  # Dictionary to store nodes with their attributes
        "edges": []   # List to store edges between nodes
    }

    /* This code populates a graph with nodes representing users and their posts, and edges representing the relationships between them. For each user in the social media data, it creates a user node and post nodes, then connects them with edges to indicate authorship, commenting, and viewing activities. This structure organizes the social media interactions into a graph format, enabling further analysis of the relationships between users and posts. */

    for user, details in social_media_data["users"].items():
        graph["nodes"][user] = {
            "type": "user",
            "posts": details["posts"],
            "comments": details["comments"],
            "views": details["views"],
            "attributes": details["attributes"]
        }
        for post in details["posts"]:
            graph["nodes"][post["post_id"]] = {
                "type": "post",
                "content": post["content"],
                "comments": post["comments"],
                "views": post["views"]
            }
            graph["edges"].append({"from": user, "to": post["post_id"], "type": "authored"})
        for comment in details["comments"]:
            graph["edges"].append({"from": user, "to": comment, "type": "commented"})
        for view in details["views"]:
            graph["edges"].append({"from": user, "to": view, "type": "viewed"})

    /* The `add_quoted_referred_edges` function adds edges to the graph that represent when one post quotes or refers to another. It checks each post node for `quoted_post_id` or `referred_post_id`, and if those referenced posts exist in the graph, it creates corresponding `"quoted"` or `"referred"` edges. This enhances the graph by capturing direct relationships between posts based on quoting and referring actions. */

    def add_quoted_referred_edges(graph):
        for node_id, node_data in graph["nodes"].items():
            if node_data["type"] == "post":
                if "quoted_post_id" in node_data:
                    quoted_post_id = node_data["quoted_post_id"]
                    if quoted_post_id in graph["nodes"]:
                        graph["edges"].append({"from": node_id, "to": quoted_post_id, "type": "quoted"})
                if "referred_post_id" in node_data:
                    referred_post_id = node_data["referred_post_id"]
                    if referred_post_id in graph["nodes"]:
                        graph["edges"].append({"from": node_id, "to": referred_post_id, "type": "referred"})

    /* This code adds relationships between specific posts in the `social_media_data`. It sets `user1`'s first post to quote `user2`'s post with `post_id` 3, and sets `user2`'s first post to refer to `user1`'s post with `post_id` 1. These relationships can then be captured in the graph as `"quoted"` and `"referred"` edges. */

    social_media_data["users"]["user1"]["posts"][0]["quoted_post_id"] = 3
    social_media_data["users"]["user2"]["posts"][0]["referred_post_id"] = 1

    /* This code initializes a graph with empty nodes and edges, then populates it with user and post nodes from `social_media_data`. It adds edges to represent relationships between users and their posts (authored), comments (commented), and views (viewed). Finally, it improve the graph with additional edges for posts that quote or refer to other posts using the `add_quoted_referred_edges` function. */

    graph = {
        "nodes": {},
        "edges": []
    }

    for user, details in social_media_data["users"].items():
        graph["nodes"][user] = {
            "type": "user",
            "posts": details["posts"],
            "comments": details["comments"],
            "views": details["views"],
            "attributes": details["attributes"]
        }
        for post in details["posts"]:
            graph["nodes"][post["post_id"]] = {
                "type": "post",
                "content": post["content"],
                "comments": post["comments"],
                "views": post["views"]
            }
            graph["edges"].append({"from": user, "to": post["post_id"], "type": "authored"})
        for comment in details["comments"]:
            graph["edges"].append({"from": user, "to": comment, "type": "commented"})
        for view in details["views"]:
            graph["edges"].append({"from": user, "to": view, "type": "viewed"})

    add_quoted_referred_edges(graph)

    /* The `highlight_important_posts` function identifies the most important posts based on a specified basis (default is `'views'`). It collects posts from the graph, retrieves their values for the given basis, and stores them in a list. The list is then sorted in descending order by the basis value, and the function returns the top 10 most important posts. */

    def highlight_important_posts(graph, criterion='views'):
        important_posts = []
        for node_id, node_data in graph["nodes"].items():
            if node_data["type"] == "post":
                important_posts.append((node_id, node_data[criterion]))
        important_posts.sort(key=lambda x: x[1], reverse=True)
        return important_posts[:10]  # Return top 10 important posts

    /* The `highlight_interesting_users` function identifies users who are notable based on specified criteria. It iterates through user nodes in the graph and calculates the sum of each criterion (e.g., comments, views) across their posts. The function collects these sums into a dictionary for each user and returns a list of tuples with user IDs and their associated criteria data. */

    def highlight_interesting_users(graph, criteria):
        interesting_users = []
        for node_id, node_data in graph["nodes"].items():
            if node_data["type"] == "user":
                user_data = {crit: sum(post[crit] for post in node_data["posts"]) for crit in criteria}
                interesting_users.append((node_id, user_data))
        return interesting_users

    /* The `highlight_trending_posts` function identifies posts that are currently trending based on a calculated score. It iterates through post nodes in the graph, calculates a score for each post by doubling the number of comments and adding the number of views, and then appends these scores to a list. The list is sorted in descending order by score, and the function returns the top 10 trending posts. */
    
    def highlight_trending_posts(graph):
        trending_posts = []
        for node_id, node_data in graph["nodes"].items():
            if node_data["type"] == "post":
                score = node_data["comments"] * 2 + node_data["views"]
                trending_posts.append((node_id, score))
        trending_posts.sort(key=lambda x: x[1], reverse=True)
        return trending_posts[:10]  # Return top 10 trending posts

    /* The `filter_posts` function filters posts based on optional keyword and user attribute criteria. It first identifies users matching the given attributes or includes all users if no attributes are specified. It then filters the posts of these users based on whether they contain include or exclude keywords and returns the filtered posts. */

    def filter_posts(graph, include_keywords=None, exclude_keywords=None, user_attributes=None):
        filtered_posts = []
    
        if user_attributes:
            valid_users = set()
            for user_id, user_data in graph["nodes"].items():
                if user_data["type"] == "user":
                    user_matches = all(user_data["attributes"].get(attr) == value for attr, value in user_attributes.items())
                    if user_matches:
                        valid_users.add(user_id)
        else:
            valid_users = set(graph["nodes"].keys())
    
        for user_id in valid_users:
            user_data = graph["nodes"].get(user_id)
            if user_data and "posts" in user_data:
                for post in user_data["posts"]:
                    content = post["content"]
                    if include_keywords and not any(keyword in content for keyword in include_keywords):
                        continue
                    if exclude_keywords and any(keyword in content for keyword in exclude_keywords):
                        continue
                    filtered_posts.append(content)
    
        return filtered_posts

    /* The `generate_word_cloud` function creates a word cloud from a list of filtered posts by combining them into a single text string. It uses the `WordCloud` class to generate a visual representation of word frequency and displays it with `matplotlib`. The resulting word cloud is shown with a white background and without axis lines for a clear view of the most frequent words. */

    def generate_word_cloud(filtered_posts):
        text = ' '.join(filtered_posts)
        wordcloud = WordCloud(width=800, height=400, background_color='white').generate(text)
    
        plt.figure(figsize=(10, 5))
        plt.imshow(wordcloud, interpolation='bilinear')
        plt.axis('off')
        plt.show()

    /* The `include_keywords` list specifies that posts must contain the word "world" to be included. The `exclude_keywords` list specifies that posts containing the word "second" should be excluded. The `user_attributes` dictionary filters posts to include only those from female users in North America. */

    include_keywords = ["world"]  # Only include posts containing "world"
    exclude_keywords = ["second"]  # Exclude posts containing "second"
    user_attributes = {"gender": "female", "region": "North America"}  # Filter by user attributes

    /*This code first uses the `filter_posts` function to obtain posts from the graph that meet the specified criteria: containing "world," not containing "second," and from users who are female and located in North America. It then generates and displays a word cloud based on these filtered posts using the `generate_word_cloud` function, visually representing the frequency of words in the selected posts. */

    filtered_posts = filter_posts(graph, include_keywords=include_keywords, exclude_keywords=exclude_keywords, user_attributes=user_attributes)
    generate_word_cloud(filtered_posts)

    /* This code retrieves key insights from the graph data by identifying important posts based on view count, interesting users based on total comments and views, and trending posts based on a combined score of comments and views. It uses the `highlight_important_posts` function to get top posts by views, `highlight_interesting_users` to find users with high engagement, and `highlight_trending_posts` to rank posts by a calculated score. These analyses help in understanding which posts and users are most significant and trending. */

    important_posts = highlight_important_posts(graph, criterion='views')
    interesting_users = highlight_interesting_users(graph, criteria=['comments', 'views'])
    trending_posts = highlight_trending_posts(graph)

    /* The `display_results` function prints out three categories of data: important posts with their IDs and importance values, interesting users with their IDs and engagement data, and trending posts with their IDs and scores. It formats each piece of information for easy reading. The function is executed to display the results of the earlier analyses. */

    def display_results(important_posts, interesting_users, trending_posts):
        print("Important Posts:")
        for post_id, value in important_posts:
            print(f"Post ID: {post_id}, Importance: {value}")

        print("\nInteresting Users:")
        for user_id, user_data in interesting_users:
            print(f"User ID: {user_id}, Data: {user_data}")

        print("\nTrending Posts:")
        for post_id, score in trending_posts:
            print(f"Post ID: {post_id}, Score: {score}")

    display_results(important_posts, interesting_users, trending_posts)
