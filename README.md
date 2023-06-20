import matplotlib.pyplot as plt
import networkx as nx

# Create the network graph
G = nx.Graph()

# Define the categories and subcategories
categories = {
    'Commercial goods and services': {
        'Healthcare & Wellbeing': ['Hospital', 'Pharmacy', 'Clinic'],
        'Education': ['School', 'University', 'Library'],
        'Environment': ['Green spaces', 'Waste management', 'Pollution control'],
        'Financial services': ['Bank', 'Insurance', 'Investment'],
        'Housing': ['Residential buildings', 'Affordable housing', 'Real estate'],
        'Food': ['Restaurants', 'Supermarkets', 'Farmers markets'],
        'Media & Entertainment': ['Theater', 'Cinema', 'Museum'],
        'Mobility': ['Public transportation', 'Bicycle lanes', 'Parking'],
        'Tech & Digital': ['Internet access', 'Data centers', 'Innovation hubs'],
        'Tourism & Hospitality': ['Hotels', 'Tourist attractions', 'Convention centers'],
        'Retail': ['Shopping malls', 'Department stores', 'Local markets']
    },
    'Public infrastructure and services': {
        'Immigration & Residency': ['Visa processing', 'Residential permits'],
        'Security & Emergency': ['Police stations', 'Fire departments', 'Emergency services'],
        'Municipal': ['City hall', 'Government offices', 'Public administration'],
        'Tax & Customs': ['Tax office', 'Customs office', 'Revenue collection'],
        'Permits & Court Resolution': ['Permit application', 'Legal advice'],
        'Public Spaces Maintenance': ['Parks maintenance', 'Street cleaning'],
        'Public Transport': ['Bus stops', 'Train stations', 'Metro lines'],
        'Environment Protection': ['Nature reserves', 'Ecological conservation']
    }
}

# Add nodes and edges to the graph
for category, subcategories in categories.items():
    G.add_node(category, size=10)
    for subcategory, nodes in subcategories.items():
        G.add_node(subcategory, size=5)
        G.add_edge(category, subcategory)
        for node in nodes:
            G.add_node(node, size=1)
            G.add_edge(subcategory, node)

# Calculate the node sizes based on the number of connections
node_sizes = [len(list(G.neighbors(node))) for node in G.nodes()]
node_sizes = [size * 300 for size in node_sizes]  # Adjust scaling factor as needed

# Plot the graph
pos = nx.spring_layout(G, seed=42)
plt.figure(figsize=(12, 8))
nx.draw_networkx(G, pos, node_size=node_sizes, alpha=0.8, with_labels=True)
plt.axis('off')
plt.show()
