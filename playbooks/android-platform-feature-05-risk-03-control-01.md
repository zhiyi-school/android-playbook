## android-platform-feature-05-risk-03-control-01

### Title

Prevent on-screen text capture

### Description

Prevent on-screen text capture by setting android:importantForAccessibility=”noHideDescendants”on views in the layout XML. This prevents the view and all its child views from being exposed to accessibility services, blocking events that could otherwise be used to read sensitive text

### Demonstration

#### 01. Prevent on-screen text capture

Prevent on-screen text capture by setting android:importantForAccessibility=”noHideDescendants”on views in the layout XML. This prevents the view and all its child views from being exposed to accessibility services, blocking events that could otherwise be used to read sensitive text

*Code excerpt from the screenshot (partial):*

```xml
<!-- Top Bar - PROTECTED: Hidden from accessibility (FX02b-C01) -->
<com.google.android.material.card.MaterialCardView
    android:id="@+id/card_top_bar"
    android:layout_width="0dp"
    android:layout_height="wrap_content"
    app:layout_constraintTop_toTopOf="parent"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    app:cardElevation="4dp"
    app:cardBackgroundColor="@color/primary_blue"
    android:importantForAccessibility="noHideDescendants">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        android:padding="16dp">

        <TextView
            android:id="@+id/tv_welcome"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/welcome_message"
            android:textColor="@color/white"
            android:textSize="20sp"
            android:textStyle="bold" />

        <TextView
            android:id="@+id/tv_balance_label"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/balance_label"
            android:textColor="@color/white"
            android:textSize="14sp"
            android:layout_marginTop="8dp" />

        <TextView
            android:id="@+id/tv_balance"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/balance_value"
            android:textColor="@color/white"
            android:textSize="32sp"
            android:textStyle="bold"
            android:layout_marginTop="4dp" />
    </LinearLayout>
</com.google.android.material.card.MaterialCardView>

<!-- Recent Transactions Card - PROTECTED: Hidden from accessibility (FX02b-C01) -->
<com.google.android.material.card.MaterialCardView
    android:id="@+id/card_transactions"
    android:layout_width="0dp"
    android:layout_height="wrap_content"
    app:layout_constraintTop_toBottomOf="@id/card_top_bar"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    android:layout_margin="16dp"
    app:cardElevation="2dp"
    app:cardCornerRadius="8dp"
    android:importantForAccessibility="noHideDescendants">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
```
