# MultiLoader Template

This project provides a Gradle project template that can compile mods for multiple modloaders using a common sourceset. This project does not require any third party libraries or dependencies. If you have any questions or want to discuss the project join our [Discord](https://discord.myceliummod.network).

## Getting Started

### IntelliJ IDEA
This guide will show how to import the MultiLoader Template into IntelliJ IDEA. The setup process is roughly equivalent to setting up the modloaders independently and should be very familiar to anyone who has worked with their MDKs.

1. Clone or download this repository to your computer.
2. Configure the project by editing the `gradle.properties` file.
3. Configure the `build.yml` and `publish.yml` files with the proper name and link.
4. Configure the mod id in the neoforge `build.gradle` file in the mods block.
5. Open the template's root folder as a new project in IDEA. This is the folder that contains this README file and the gradlew executable.
6. If your default JVM/JDK is not Java 21 you will encounter an error when opening the project. This error is fixed by going to `File > Settings > Build, Execution, Deployment > Build Tools > Gradle > Gradle JVM` and changing the value to a valid Java 21 JVM. You will also need to set the Project SDK to Java 21. This can be done by going to `File > Project Structure > Project SDK`. Once both have been set open the Gradle tab in IDEA and click the refresh button to reload the project.
7. Configure the packages and classes in the `src` folder to match your mod.
8. Open your Run/Debug Configurations. Under the Application category there should now be options to run NeoForge and Fabric projects. Select one of the client options and try to run it.
9. Assuming you were able to run the game in step 7 your workspace should now be set up.

## Development Guide
When using this template the majority of your mod is developed in the Common project. The Common project is compiled against the vanilla game and is used to hold code that is shared between the different loader-specific versions of your mod. The Common project has no knowledge or access to ModLoader specific code, apis, or concepts. Code that requires something from a specific loader must be done through the project that is specific to that loader, such as the NeoForge or Fabric project.

Loader specific projects such as the NeoForge and Fabric project are used to load the Common project into the game. These projects also define code that is specific to that loader. Loader specific projects can access all of the code in the Common project. It is important to remember that the Common project can not access code from loader specific projects.

## Removing Platforms and Loaders
While the MultiLoader Template includes support for many platforms and loaders you can easily remove support for the ones you don't need. This can be done by deleting the subproject folder and then removing it from the `settings.gradle` file. For example if you wanted to remove support for Forge you would follow the following steps. 

1. Delete the subproject folder. For example, delete `MultiLoader-Template/forge`.
2. Remove the project from `settings.gradle`. For example, remove `include("forge")`. 
