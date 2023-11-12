---
title: "Sorting Arrays with JavaScript: A Guide to Proper Numerical Order"
date: 2023-11-11 00:00:00
description: Explore effective techniques for numerical sorting in JavaScript. From overcoming default sorting challenges to ensuring a natural order, master the art of effortlessly organizing arrays of strings.
featured_image: "/images/posts/2023-11-11-sorting-arrays-with-javascript/featured-image.png"
attribution: '<a href="https://www.freepik.com/free-vector/sorting-thoughts-concept-illustration_12780668.htm#query=sorting&position=0&from_view=search&track=sph">Image by storyset</a> on Freepik'
---

I was recently working on a project that required sorting an array of strings, each string containing a crucial number. The catch? The strings needed to be arranged in order according to those numbers. I immediately defaulted to JavaScript's built-in sorting method, `Array.prototype.sort()`, but that didn't work out quite as expect.

## The Default Sort Trap

Let's take a look at a classic example:

```javascript
const mixedArray = ["item10", "item2", "item1"];

// Using Array.prototype.sort()
const regularSort = mixedArray.slice().sort();
console.log("Regular Sort:", regularSort); // Result: ["item1", "item10", "item2"]
```

Why does this happen? The default `Array.prototype.sort()` method uses string comparison by default, treating the array elements as strings and sorting them lexicographically. This means that "item10" comes before "item2" because "1" comes before "2" in string order.

## Enter Intl.Collator for Proper Numerical Sorting

To remedy this, we introduce the `Intl.Collator` object with numeric options:

```javascript
const mixedArray = ["item10", "item2", "item1"];

// Using Intl.Collator for a more natural order
const collator = new Intl.Collator(undefined, { numeric: true });
const collatorSort = mixedArray.slice().sort(collator.compare);
console.log("Collator Sort:", collatorSort); // Result: ["item1", "item2", "item10"]
```

In this example, we use "undefined" for the `locales` parameter. This means the default locale is used. In the context of numerical sorting, specifying a locale might be relevant if you want to tailor the sorting to the conventions of a specific language or region.

## Understanding Intl.Collator

What exactly is this `Intl.Collator`? According to the [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/Collator), it's an object that enables language-sensitive string comparison. In simpler terms, we can sort strings based on a locale's language.

Let's briefly delve into the key parameters of the `Intl.Collator()` constructor that will provide numerical sorting:

- **locales:** This parameter determines the locale or locales whose collation rules should be used. For numerical sorting, you might specify a locale that aligns with your desired numeric ordering. In our example, we use "undefined" to indicate the default locale.
- **sensitivity:** The sensitivity parameter influences the comparison's sensitivity to case, diacritics, and other linguistic variations. In the context of numerical sorting, you might adjust sensitivity based on whether you want to distinguish between, say, uppercase and lowercase.
- **numeric:** The numeric parameter, our star in numerical sorting, when set to `true`, ensures that the comparison is numeric, not lexicographic. This is what makes `Intl.Collator` a game-changer for our sorting needs.

For a deeper dive into all the possible parameters, check the full list [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/Collator/Collator).

## The compare Method

Now, let's talk about the `compare` method of `Intl.Collator`. When we use `collator.compare` in the `sort` function, we're telling JavaScript to use the collator's comparison algorithm for sorting. This method considers the specified locale and options, ensuring a proper numerical order.

## Conclusion

In a nutshell, while JavaScript's default sorting might trip you up when dealing with strings containing numbers, `Intl.Collator` steps in as the hero. By embracing its numeric options and leveraging the `compare` method, you can achieve the proper numerical order your project demands. Happy sorting!
