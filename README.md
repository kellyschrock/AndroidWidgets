Android Widgets
==============

Various Android widgets
--------------


This is a library I hope to add to over time, a place to keep custom views that turn out useful.



TouchMagView
============
TouchMagView is a magnifier view for Android apps. Typical usage is to place it at the top
of the z-order in a RelativeLayout. By default, it does nothing, until you attach one or
more other views to it, and call the startMagnifying() method. At that point a loupe
of a size and magnification you specify appears where you're touching, and magnifies that
area.

Here's a picture of it in action:

![Screenshot] (resources/screenshot.png?raw=true "Magnifier")

To use it, do something like this in a layout:

    <RelativeLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        >
        <ImageView
            android:id="@+id/some_img"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:src="@drawable/some_image"
            />
            
        <com.fognl.android.widget.TouchMagView
            android:id="@+id/mag"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            />
    </RelativeLayout>

Then, in onCreate() of the Activity, do something like this:

        mMagView = (TouchMagView)findViewById(R.id.magnifier);
        mMagView
            // Add a view to magnify
            .addView(findViewById(R.id.img))
            // Set the size of the loupe (px)
            .setLoupeSize(200)
            // Set the magnification
            .setZoom(2f)
            // Display it 200px above the touch point (helps if you want to see it!)
            .setXYOffsets(0, -200)
            // Pass touch events to the views under the magnifier
            .setListener(new TouchMagView.Listener() {
                @Override
                public void onTouchEvent(MotionEvent event) {
                    // Pass the event through to the relevant views.
                    findViewById(R.id.img).dispatchTouchEvent(event);
                }
            });

You can specify when to start and stop magnifying. For example:

    public void onStartMagClick(View v) {
        mMagView.startMagnifying();
    }
    
    public void onStopMagClick(View v) {
        mMagView.stopMagnifying();
    }
    
There are several options for controlling loupe size, magnification, various colors (rim, text, crosshair), whether or not to show a crosshair or text, etc.

More to come.

Project Structure
=================
The library/ directory contains the Android library you'll (perhaps) use in your project. The demo/ directory contains an app that shows it in action.

Have fun.


