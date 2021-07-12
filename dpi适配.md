/**
* 屏幕适配
* 设计图宽360dp
*/
private static float sNoncompatDensity;
private static float sNoncompatScaledDensity;
private static void setCustomDensity(@NonNull Activity activity, @NonNull final Application application) {
    DisplayMetrics appDisplayMetrics = application.getResources().getDisplayMetrics();
    if (sNoncompatDensity == 0) {
        sNoncompatDensity = appDisplayMetrics.density;
        sNoncompatScaledDensity = appDisplayMetrics.scaledDensity;
        application.registerComponentCallbacks(new ComponentCallbacks() {
            @Override
            public void onConfigurationChanged(Configuration newConfig) {
                if (newConfig != null && newConfig.fontScale > 0) {
                    sNoncompatScaledDensity = application.getResources().getDisplayMetrics().scaledDensity;
                }
            }

            @Override
            public void onLowMemory() {

            }
        });
    }
    float targetDensity = appDisplayMetrics.widthPixels / 360;
    float targetScaledDensity = targetDensity * (sNoncompatScaledDensity / sNoncompatDensity);
    int targetDensityDpi = (int) (160 * targetDensity);

    appDisplayMetrics.density = targetDensity;
    appDisplayMetrics.scaledDensity = targetScaledDensity;
    appDisplayMetrics.densityDpi = targetDensityDpi;

    DisplayMetrics activityDisplayMetrics = activity.getResources().getDisplayMetrics();
    activityDisplayMetrics.density = targetDensity;
    activityDisplayMetrics.scaledDensity = targetScaledDensity;
    activityDisplayMetrics.densityDpi = targetDensityDpi;
}
