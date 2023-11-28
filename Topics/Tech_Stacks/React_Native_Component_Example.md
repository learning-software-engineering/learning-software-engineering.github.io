# Example Implementation of React Native Components

This guide provides a quick demonstration on how to write customized components as part of the application page content in React Native.

## Table of Contents
-  **[Setup](#setup)**
-  **[Create Custom Component](#create_component)**
-  **[Using ProductCard Component](#product_card)**
-  **[Running the App](#running_app)**
-  **[Further Customization](#further_customization)**

### Step 1: Setup <a id="setup"></a>

Ensure you have Node.js, npm or Yarn, and React Native CLI installed on your machine.

```jsx
# Install  React  Native  CLI  globally
npm  install -g  react-native-cli
```
Create a new React Native project:

```jsx
npx react-native init MyCustomComponentsApp
cd MyCustomComponentsApp
```

### Step 2: Create Custom Component <a id="create_component"></a>

In this demonstration, we will create a custom product card component designed to contain product information.

1.  **Create a New File:** Inside your project directory, create a new file for the product card component, e.g., `ProductCard.js`.
    
2.  **Write the Custom Component:**
```jsx
 // ProductCard.js

import React from 'react';
import { View, Text, Image, StyleSheet } from 'react-native';

const ProductCard = ({ product }) => {
  const { name, price, image } = product;

  return (
    <View style={styles.card}>
      <Image source={{ uri: image }} style={styles.image} />
      <View style={styles.cardDetails}>
        <Text style={styles.productName}>{name}</Text>
        <Text style={styles.productPrice}>${price}</Text>
      </View>
    </View>
  );
};
const styles = StyleSheet.create({
  card: {
    backgroundColor: '#fff',
    borderRadius: 8,
    elevation: 3,
    shadowOffset: { width: 1, height: 1 },
    shadowColor: '#333',
    shadowOpacity: 0.3,
    marginHorizontal: 4,
    marginVertical: 6,
  },
  image: {
    width: '100%',
    height: 200,
    borderTopLeftRadius: 8,
    borderTopRightRadius: 8,
  },
  cardDetails: {
    padding: 10,
  },
  productName: {
    fontSize: 18,
    marginBottom: 5,
  },
  productPrice: {
    fontSize: 16,
    color: '#888',
  },
});

export default ProductCard;
```

### Step 3: Using ProductCard Component <a id="product_card"></a>

Now, you can use the `ProductCard` component in your app.

**Import Custom Component:**
```jsx
// App.js

import React from 'react';
import { View, StyleSheet } from 'react-native';
import ProductCard from './ProductCard'; // Import the ProductCard component

const App = () => {
  // sample product data (replace this with your actual product data)
  const products = [
    {
      id: 1,
      name: 'Banana',
      price: 2.99,
      image: 'https://samplefruits.com/123', // Replace with your image URL
    },
    // Add more products as needed
  ];
  return (
    <View style={styles.container}>
      {products.map((product) => (
        // Render ProductCard component for each product
        <ProductCard key={product.id} product={product} /> // Our product card component
      ))}
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#f0f0f0',
    padding: 10,
  },
});

export default App;
```

### Step 4: Running the App <a id="running_app"></a>

Run your React Native application:
```jsx
npx react-native run-android    # For Android
# or
npx react-native run-ios        # For iOS
```
This will launch your app in the emulator or on a connected device, and you will see your customized ProductCard component rendered on the screen for each product in the `products` array.

### Step 5: Further Customization <a id="further_customization"></a>

Feel free to customize the `ProductCard` component further by adding props, styling options, or additional functionality based on your application's requirements.

This approach can be extended to create various customized components for different parts of your application, enhancing reusability and maintainability.

Remember to test your components thoroughly to ensure they work as expected in various scenarios.