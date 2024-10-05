# Smart Wear

## I. Preface
Many people struggle to match clothes in a full closet. Our survey[^1] reveals common challenges: feeling overwhelmed by fashion, wanting to pair new purchases with existing clothes, dressing inappropriately for the weather, taking too long to decide on outfits for special occasions, and finding trying on clothes cumbersome. This inspired us to develop "SmartWear," a smart outfit tool that helps users easily find the perfect match, boosting their confidence and style for any occasion. Whether you're a fashion novice or facing decision fatigue, SmartWear simplifies outfit choices and helps you look great every day!

## II. Innovation Description
SmartWear matches the upper and lower garments into stylish outfits, significantly reducing decision-making time. Our survey shows that people take over three times longer to choose outfits for special occasions than on regular days, 90% have dressed inappropriately for the weather at least once, and over half want to see how new clothes pair with their wardrobe. To address these issues, our system automatically adjusts outfit recommendations based on occasions, weather, and selected clothing items.

Additionally, we integrated features that garnered over 50% support in our survey. "Smart Semantic Matching" lets users input thoughts via text or voice, and the system suggests outfits based on semantics. The "Virtual Try-on" feature allows users to visualize how clothes would look on them. Lastly, "Clothing Usage Analysis" helps users identify frequently and rarely worn items, assisting in decisions on what to keep or discard.

Combining these features, SmartWear offers a customized experience for defining outfit conditions, providing outfit recommendations, and visualizing looks in one seamless process.

## III. System Functions
The key system pages are shown in Figure 1. We will introduce the more complex functions, with the blue labels in the image corresponding to the numbered points below.

<p align="center" width="1200">
  <img alt="image" src="https://github.com/user-attachments/assets/f22e9586-e04b-4b26-95cc-07829cc9f7f1">
  <p align="center">▲ Figure 1: Key System Interface Diagram</p>
</p>

1. **Upload Photos to Closet**: Users can upload images of individual clothing items or full outfits. The system automatically recognizes the clothing attributes, separates upper and lower garments, and organizes them in the closet.
2. **Customizable Outfit Recommendations**: Users can specify different conditions, and the system will generate outfit suggestions sorted based on a scoring system.  
   - **Based on Semantic**: Users can input requests through text or voice (e.g., "I want to look cute"), and the system will suggest clothing attributes that match the semantics of the input.  
   - **Based on Occasion, Weather, and Clothing**: Users can select occasions (e.g., daily work and conference), decide whether to consider the system's automatic weather data, and specify an upper or lower garment for pairing.
3. **Virtual Try-on**: Users can upload their photos to try on selected outfits or individual items virtually.
4. **Clothing Usage Analysis**: Users can view frequently and rarely worn clothes, helping them assess wardrobe usage and decide what to keep or discard.

## IV. System Features
- **Easy Upload and Automatic Clothing Recognition**: Users can upload individual garments or full outfit photos, and the system automatically removes faces or backgrounds, retaining only the clothing and splitting them into upper and lower garments. The system automatically extracts clothing names and attributes without manual input.
- **Customizable Matching Conditions**: Users can choose whether to consider occasions, weather, or specific clothing items. They can also use natural language input, allowing the system to adjust the outfit recommendations accordingly.
- **Efficient and Streamlined Experience**: The system filters out unsuitable clothes, generates recommendations, and provides virtual try-on capabilities, saving users time and making the process quick and user-friendly.
- **More Innovative and Practical Than Existing Apps**: Existing smart outfit apps often require users to manually input clothing attributes and occasions, typically considering only weather conditions for outfit suggestions, which are displayed as simple photo collages. In contrast, SmartWear incorporates user feedback to customize outfit recommendations based on weather, occasions, selected items, and semantic input—all without manual data entry. After generating outfit recommendations, users can virtually try on outfits, enhancing the planning experience.

## V. System Development Tools and Techniques
The system architecture is shown in Figure 2. The front end is developed using React Native, while the back end uses Python's FastAPI framework. The database is PostgreSQL, and the deep learning frameworks are TensorFlow and PyTorch. Aside from our models, we also use the clothing recognition model DeepFashion2, the language model Gemini, the virtual try-on model IDM-VTON, and a weather API.

<p align="center" width="1200">
  <img alt="image" src="https://github.com/user-attachments/assets/612f764c-3615-4f3a-8be9-5f1909f37bec">
  <p align="center">▲ Figure 2: System Architecture Diagram</p>
</p>

Figure 3 illustrates the key system processes. We will introduce the more technically challenging parts, with the blue box labels corresponding to the numbered points below.

<p align="center" width="1200">
  <img alt="image" src="https://github.com/user-attachments/assets/7764d2e3-08a6-4313-a436-438927eb9647">
  <p align="center">▲ Figure 3: Key System Process Diagram</p>
</p>

1. **Extract Clothing Attributes from Photos**: We use DeepFashion2[^2], a well-known multi-task clothing recognition model, to remove backgrounds, separating upper and lower garments. The Gemini model then extracts attributes like patterns.
2. **Filter Clothes Based on Occasions**: We crawled IG for 5,132 outfit photos tagged by occasion, then used the point 1 method to extract clothing attributes and aggregated them as filters.
3. **Filter Clothes Based on Weather**: The system uses a weather API to retrieve local temperatures. Following the "26-Degree Dressing Rule," suitable clothing attributes are selected.
4. **Filtering Clothes Based on Selected Items**: If the user specifies an upper or lower garment, the system considers only pairing options with the selected item.
5. **Learning Outfit Combinations from Datasets and Models**: We collected 3,440 outfit photos from WEAR and used DeepFashion2 to split them into upper and lower garments. The original combinations were labeled as "good" outfits and shuffled ones as "bad," forming the dataset. Then, the Gemini model provided garment descriptions, and BERT with neural networks learned pairing rules. Outfits are ranked based on model scores.
6. **Smart Semantic Matching**: Voice input converted to text is processed via Gemini to identify relevant clothing attributes.
7. **Virtual Try-on**: We use IDM-VTON[^3], a virtual try-on model that excels in preserving garment details and generating realistic images, to overlay clothing onto the user's photo.

## VI. System Users
SmartWear is designed for anyone with outfit concerns—beginners, those with decision fatigue, or anyone needing outfit inspiration for occasions or weather. It's intuitive and easy to use, even for users who are not tech-savvy. The system is free for general users, and it may add commercial value if we have a win-win collaboration with fashion retailers by offering analyzed customer preferences, personalized recommendations, and virtual try-on features, enhancing customer satisfaction and driving sales.

## VII. System Environment
The system runs on iOS, Android, or browser-enabled smartphones. Since the system connects to weather and model APIs, users need an internet connection and permission to access location services to enjoy the full features.

## VIII. Conclusion
SmartWear is an intelligent outfit system that uses API integrations and machine learning to provide personalized outfit recommendations and virtual try-on experiences based on weather, occasions, selected clothing items, and semantics. It simplifies the process of choosing suitable outfits, making fashion fun and simple. With SmartWear, everyone can wear outfits in a smart way!

## References
[^1]: SmartWear Team, "Survey on the Demand for Smart Outfit Services." Available: <https://docs.google.com/spreadsheets/d/1jDKOoPwypNMAlZvOFrRYdc-LbZbftvBfEyqbKO9iBII/edit?usp=sharing>.
[^2]: Y. Ge, R. Zhang, X. Wang, X. Tang, and P. Luo, "DeepFashion2: A Versatile Benchmark for Detection, Pose Estimation, Segmentation and Re-Identification of Clothing Images," 2019 IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR), 2019, pp. 5332-5340, doi: 10.1109/CVPR.2019.00548.
[^3]: Y. Choi, S. Kwak, K. Lee, H. Choi, and J. Shin, "Improving diffusion models for authentic virtual try-on in the wild," arXiv:2403.05139 [cs.CV], 2024.
