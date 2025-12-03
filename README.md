# Identifying_Key_Entities_in_Recipe_Data
The CRF model performs strongly on the validation dataset with an overall token-level accuracy of 98.16%. The classification report and confusion matrix highlight a high level of consistency across all three entity types—ingredient, quantity, and unit—with especially strong performance on high-support classes.

1. Ingredient Labels

- Highest accuracy: 99.38%
- Very few mistakes (13 out of 2107 tokens).
- Most ingredient errors involve tokens like "cloves" or "pieces" incorrectly predicted as unit due to their dual semantic usage in cooking contexts (e.g., “3 cloves garlic”).
- Since "cloves" and "pieces" frequently behave like units in natural language, misclassification is understandable.

2. Quantity Labels

- Accuracy of 98.54%.
- Errors mostly occur when the model confuses quantity tokens such as “few” or “3” with ingredient or unit labels, especially when the surrounding context is ambiguous.
- Example: “few Leaves” → “few” predicted as quantity instead of ingredient due to misleading context structure.

3. Unit Labels

- Lowest accuracy: 90.50%
- Units account for 34 of the 53 total errors, making them the weakest component.
- Units like “spoon”, “cloves”, “pieces” are often confused with ingredient labels.
- These errors typically occur when:
- The unit is not part of the predefined unit_keywords.
- The unit token looks like a noun that could also be an ingredient.
- The model lacks contextual cues from noisy or incomplete sentences.

4. General Misclassification Patterns

- Ingredient ↔ Unit swaps are the most common type of error (especially for multi-use nouns).
- Tokens with weak preceding quantities (e.g., “big oil”, “seeds garlic”) cause confusion.
- Some tokens like “few”, categorized as quantity keywords, are labeled as ingredients depending on the dataset annotation rules.
- Sentences with irregular formatting or missing delimiters increase error frequency.

5. Class Weight Impact

- Unit class had the highest class weight (~8.77), reflecting its rarity and helping the model learn better.
- Despite high weight, the model still finds unit detection challenging, suggesting:
- Need for broader unit keyword list.
- Additional features for noun-based units.
- Possibly richer context windows or dependency-based features.
