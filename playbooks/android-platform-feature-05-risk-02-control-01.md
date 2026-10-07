## android-platform-feature-05-risk-02-control-01

### Title

Prevent user activities from being captured

### Description

Insert here

### Demonstration

#### 01. Prevent user activities from being captured

Prevent user activities from being captured by accessibility services by setting android:importantForAccessibility="no" on views in the layout XML. This stops TYPE_VIEW_TEXT_CHANGED events from being sent for that view, so text input cannot be captured

```xml
<com.google.android.material.textfield.TextInputLayout
    android:id="@+id/til_username"
    android:layout_width="0dp"
    android:layout_height="wrap_content"
    app:layout_constraintTop_toBottomOf="@id/tv_title"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    android:layout_marginTop="60dp"
    app:boxBackgroundMode="outline"
    android:importantForAccessibility="no"> <!-- Username Input - PROTECTED: Hidden from accessibility (FX02a-C01) -->

    <com.google.android.material.textfield.TextInputEditText
        android:id="@+id/et_username"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="@string/username_hint"
        android:inputType="text"
        android:maxLines="1"
        android:importantForAccessibility="no" />
</com.google.android.material.textfield.TextInputLayout>

<com.google.android.material.textfield.TextInputLayout
    android:id="@+id/til_password"
    android:layout_width="0dp"
    android:layout_height="wrap_content"
    app:layout_constraintTop_toBottomOf="@id/til_username"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    android:layout_marginTop="16dp"
    app:boxBackgroundMode="outline"
    app:endIconMode="password_toggle"
    android:importantForAccessibility="no"> <!-- Password Input - PROTECTED: Hidden from accessibility (FX02a-C01) -->

    <com.google.android.material.textfield.TextInputEditText
        android:id="@+id/et_password"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="@string/password_hint"
        android:inputType="textPassword"
        android:maxLines="1"
        android:importantForAccessibility="no" />
</com.google.android.material.textfield.TextInputLayout>

<com.google.android.material.button.MaterialButton
    android:id="@+id/btn_login"
    android:layout_width="0dp"
    android:layout_height="60dp"
    android:text="@string/login_button"
    android:textSize="16sp"
    app:layout_constraintTop_toBottomOf="@id/til_password"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    android:layout_marginTop="32dp"
    android:importantForAccessibility="no" /> <!-- Login Button - PROTECTED: Hidden from accessibility (FX02a-C01) -->
```
