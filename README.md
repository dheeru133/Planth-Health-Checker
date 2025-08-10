Plant Health Checker - Android (Kotlin) - India-focused
=======================================================

What this repo contains:
- Android Studio project (app module) ready to open
- Kotlin MainActivity implementing camera/gallery image pick and TFLite inference
- assets/labels.txt (disease labels)
- assets/diseases.json (disease info + remedies for Indian crops)
- placeholder app/src/main/assets/model.tflite (REPLACE with your TFLite model)
- .github/workflows/android-build.yml (builds debug APK on push)
- Instructions to build locally and sign release APK

IMPORTANT:
- The included model.tflite is a placeholder and NOT a working model.
- To get a working app, train or obtain a TFLite model that matches labels.txt order and place it in app/src/main/assets/model.tflite
- See 'Training_and_Conversion.md' for step-by-step training and conversion guidance using public datasets (PlantVillage / Kaggle).

Next steps (quick):
1. Open the project in Android Studio and run on an emulator or device for debug testing.
2. Replace placeholder model.tflite with your real model and labels.txt if you have one.
3. To generate an APK automatically, push the repo to GitHub and enable Actions (see workflow file). Add signing keystore secrets to sign release builds if desired.
