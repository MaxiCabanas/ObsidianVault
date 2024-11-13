- [Build types](#build-types)
		- [Debug Build](#debug-build)
		- [Development Build](#development-build)
		- [Shipping Build](#shipping-build)
		- [Best Practices](#best-practices)
	- [Citations:](#citations)
- [Cooking vs Packaging](#cooking-vs-packaging)
	- [Cooked Assets](#cooked-assets)
	- [Packaged Assets](#packaged-assets)
	- [Key Differences](#key-differences)
	- [Citations:](#citations)

# Build types

In Unreal Engine 5 (UE5), there are three main types of builds: Debug Build, Development Build, and Shipping Build. Each serves a different purpose and has distinct characteristics. Let me explain the differences between them:

### Debug Build

A Debug Build is primarily used during development and testing phases [1]. Its main features include:

- Contains extensive error checking and logging
- Includes additional safety checks
- Often runs slower due to added checks and logging
- Useful for identifying and fixing bugs quickly

Key points to consider:
- Debug Builds are typically larger in size compared to other build types
- They contain symbols, which are essential for debugging but increase the build size
- Debug Builds are not recommended for final game releases

### Development Build

A Development Build is a compromise between Debug and Shipping Builds [1]. Its characteristics are:

- Faster performance compared to Debug Builds
- Less verbose logging than Debug Builds
- Still includes some safety checks and logging
- Smaller in size compared to Debug Builds

Key points to consider:
- Development Builds are suitable for internal testing and playtesting sessions
- They offer a balance between development needs and performance
- These builds are often used by QA teams for thorough testing

### Shipping Build

A Shipping Build is the final version of your game intended for release to players [1]. Its features include:

- Optimized for maximum performance
- Minimal logging and debugging information
- Smallest in size among the three build types
- Contains minimal error checking

Key points to consider:
- Shipping Builds are what players will experience in the final product
- They are designed to run smoothly on various hardware configurations
- Shipping Builds should be thoroughly tested to ensure stability and performance

### Best Practices

When working with UE5 builds:

1. Use Debug Builds for initial development and bug fixing
2. Switch to Development Builds for internal testing and playtesting
3. Optimize and test thoroughly with Shipping Builds before release
4. Always maintain separate build configurations for different stages of development
5. Regularly update and rebuild your project to catch potential issues early

By understanding and utilizing these different build types effectively, you can streamline your development process and ensure a high-quality final product for players.

## Citations:
[1] https://forums.unrealengine.com/t/whats-the-different-between-developement-build-and-a-shipping-build/113093
[2] https://www.reddit.com/r/unrealengine/comments/bgtaht/what_is_the_difference_between_development_and/
[3] https://forums.unrealengine.com/t/ue5-shipping-build-still-has-debug-features-and-console/580118
[4] https://www.youtube.com/watch?v=CmWbMT4WAhU
[5] https://www.youtube.com/watch?v=MPo4K9hE4S8
[6] https://github.com/chiefGui/ue-from-source
[7] https://rider-support.jetbrains.com/hc/en-us/community/posts/6784391005330-Differences-between-the-solution-configurations
[8] https://communityforums.atmeta.com/t5/Quest-Development/Unreal-game-launching-Assertion-failed-AsyncLoadingThread-crash/td-p/963840
[9] https://communityforums.atmeta.com/t5/Unreal-VR-Development/UE4-crash-when-using-VR-Preview-since-last-Oculus-app-update/td-p/1101828
[10] https://www.dannygoodayle.com/standing-up-horde-an-unreal-build-system/

Here's an explanation of the difference between cooked and packaged assets in Unreal Engine 5:

# Cooking vs Packaging
## Cooked Assets

Cooked assets refer to optimized versions of your game's assets that have been prepared for deployment on specific target platforms. The cooking process involves several key steps:

1. Asset Conversion: Unreal Engine converts assets into formats better suited for the target platform, including compressing textures and optimizing models [1].

2. Shader Compilation: The engine compiles shaders for the target platform's graphics API (e.g., DirectX, Vulkan, or Metal) to ensure optimal rendering performance [1].

3. Content Packaging: Cooked content is packaged into efficient file formats (e.g., PAK files) that allow quick loading during runtime [1].

4. Data Optimization: Additional optimizations may be applied, such as generating navigation data or calculating level of detail (LOD) information [1].

The cooking process focuses on preparing assets specifically for deployment on target platforms like PCs, consoles, or mobile devices [1]. This ensures optimal performance and compatibility for those platforms.

## Packaged Assets

Packaged assets refer to the process of creating distributable versions of your game for release. While related to cooked assets, packaging involves additional steps:

1. Project Assembly: Unreal Engine assembles all necessary components of your game project into a single package [1].

2. Build Configuration: The engine applies build configurations specific to the target platform.

3. Final Optimization: Any last-minute optimizations or adjustments are made.

4. Distribution Preparation: The packaged asset is prepared for distribution, including creation of installers, setup files, etc.

Unlike cooking, which optimizes individual assets, packaging creates a complete, deployable version of your game ready for distribution to end-users.

## Key Differences

1. Scope: Cooking focuses on optimizing individual assets, while packaging deals with assembling the entire game project [1].

2. Purpose: Cooking prepares assets for deployment, while packaging creates a distributable version of the entire game [1].

3. Timing: Cooking is typically done before packaging, as optimized assets need to be incorporated into the final package [1].

4. Output: Cooking produces optimized asset files, while packaging generates a complete, deployable game package [1].

In summary, cooking is about optimizing individual assets for specific platforms, while packaging is about creating a complete, distributable version of your game. Both processes are crucial for ensuring your game performs well across various platforms.

## Citations:
[1] https://medium.com/@thelazyindiantechie/whats-the-difference-between-cook-and-build-in-unreal-engine-5-d5b1271c5b06
[2] https://forums.unrealengine.com/t/cooking-packaging/378959
[3] https://forums.unrealengine.com/t/cooking-unreferenced-assets/284378
[4] https://www.gildor.org/smf/index.php?topic=7770.0
[5] https://www.youtube.com/watch?v=9MGHBU5eNu0
[6] https://www.youtube.com/watch?v=6unVb5gNBtM
[7] https://www.gildor.org/smf/index.php?topic=6526.0
[8] https://www.coconutlizard.co.uk/blog/the-cook-the-resave-his-garbage-and-her-optimization/
[9] https://stackoverflow.com/questions/78382221/packaging-an-android-game-in-unreal-5-max-memory-exceeded-goes-to-garbage-col