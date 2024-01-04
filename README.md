# MiuiCamera-veux

1. Clone the main MiuiCamera repository to `vendor/xiaomi/miuicamera`
2. Clone this repository to `vendor/xiaomi/miuicamera-veux`
3. Add the line below to `device.mk`
    ```makefile
    $(call inherit-product, vendor/xiaomi/miuicamera-veux/MiuiCamera-veux.mk)
    ```
4. Include SELinux policy in `BoardConfig.mk`
    ```makefile
    include vendor/xiaomi/miuicamera-veux/SEPolicy-veux.mk
    ```

## Technical details

`libcamera_algoup_jni.xiaomi.so` was extracted from **V14.0.4.0.TKCMIXM** and patched for **AOSP**:
```sh
patchelf --add-needed "libgui_shim_miuicamera.so" prebuilt/libcamera_algoup_jni.xiaomi.so
```
When the correct `shared_libs` list is not present in Android.bp, `check_elf_file.py` prints it on build:
```
FAILED: Check prebuilt ELF binary: out/soong/.intermediates/vendor/xiaomi/miuicamera-veux/libcamera_algoup_jni.xiaomi/android_arm64_armv8-2a-dotprod_cortex-a55_shared/libcamera_algoup_jni.xiaomi.so
...
out/soong/.intermediates/vendor/xiaomi/miuicamera-veux/libcamera_algoup_jni.xiaomi/android_arm64_armv8-2a-dotprod_cortex-a55_shared/libcamera_algoup_jni.xiaomi.so: note: Fix suggestions:
out/soong/.intermediates/vendor/xiaomi/miuicamera-veux/libcamera_algoup_jni.xiaomi/android_arm64_armv8-2a-dotprod_cortex-a55_shared/libcamera_algoup_jni.xiaomi.so: note:   Android.bp: shared_libs: ["android.hidl.token@1.0-utils", "libandroid", "libandroid_runtime", "libbase", "libbinder", "libc++", "libcamera_client", "libcamera_metadata", "libcutils", "libgui", "libgui_shim_miuicamera", "liblog", "libmedia_jni_utils", "libnativehelper", "libnativewindow", "libui", "libutils", "libvndksupport"],
```
