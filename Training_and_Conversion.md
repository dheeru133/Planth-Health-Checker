Training and Converting a Keras model to TFLite (brief)
-------------------------------------------------------
1. Collect dataset (e.g., PlantVillage, Kaggle). Create folders per class:
   train/Healthy, train/Leaf_Spot, train/Powdery_Mildew, ...
2. Use transfer learning with MobileNetV2 or EfficientNetB0 for good mobile performance.
3. Example training sketch (TensorFlow / Python):
   ```python
   base = tf.keras.applications.MobileNetV2(input_shape=(224,224,3), include_top=False, pooling='avg')
   x = base.output
   x = tf.keras.layers.Dense(128, activation='relu')(x)
   outputs = tf.keras.layers.Dense(num_classes, activation='softmax')(x)
   model = tf.keras.Model(inputs=base.input, outputs=outputs)
   model.compile(optimizer='adam', loss='sparse_categorical_crossentropy', metrics=['accuracy'])
   model.fit(train_ds, validation_data=val_ds, epochs=10)
   ```
4. Convert to TFLite with optimization (float16 quantization suggested):
   ```python
   converter = tf.lite.TFLiteConverter.from_keras_model(model)
   converter.optimizations = [tf.lite.Optimize.DEFAULT]
   converter.target_spec.supported_types = [tf.float16]
   tflite_model = converter.convert()
   open('model.tflite','wb').write(tflite_model)
   ```
5. Verify model on device with TFLite interpreter or Android test app.
