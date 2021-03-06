# FOML
 Fabric OBJ Model Loader

# Adding the API to your project

```
repositories {
    maven {
        name = "NerdHubMC"
        url = "https://maven.abusedmaster.xyz"
    }
}

dependencies {
    modCompile "com.github.NerdHubMC:FOML:${foml_version}"
    
    // Includes FOML as a Jar in Jar dependency, Optional
    include "com.github.NerdHubMC:FOML:${foml_version}"
}
```

You can find current releases over at the [maven](https://maven.abusedmaster.xyz/com/github/NerdHubMC/FOML/)

# How to use
Getting started with FOML is very simple and easy to do.

Firstly you have to register your MODID as an OBJ Model handler, so that FOML will know to load OBJ models under your mod's domain.

### **Example:**

```
OBJLoader.INSTANCE.registerDomain(MODID);
```

After you register your domain, all you have to do is specify the OBJ model in the blockstate's file as such:

```
{
    "variants": {
        "": { "model": "testmod:block/test_model.obj" }
    }
}
```

Your OBJ model and MTL files should be placed in your models package.

To make the textures in your MTL file work you must prefix the name with your modid following the location of the texture:
the blocks/ location can be replaced with any folder in the `textures` folder, note do **not** suffix the texture with .png


```
#Example MTL File

newmtl Base
Ka 0.0000 0.0000 0.0000
Kd 1.0000 1.0000 1.0000
Ks 1.0000 1.0000 1.0000
Tf 0.0000 0.0000 0.0000
d 1.0000
Ns 0.0000
map_Kd MODID:blocks/test
```

And that's basically it, your block show now render your OBJ model! **(Note: It is recommended to scale the model before exporting it due to the size it will be rendered as)**


### Using OBJ models for items

JSON-formatted vanilla item models placed in the `models/item` folder can also specify your OBJ model as its "parent" model, similar to blockstates:

```
{
    "parent": "MODID:item/test.obj",
    "display": {
        "head": {
            "rotation": [0, 0, 0],
            "translation": [0, 0, 0],
            "scale": [1, 1, 1]
        },
        "firstperson_righthand": {
            "rotation": [0, 0, 0],
            "translation": [0, 0, 0],
            "scale": [1, 1, 1]
        },
        "firstperson_lefthand": {
            "rotation": [0, 0, 0],
            "translation": [0, 0, 0],
            "scale": [1, 1, 1]
        },
        "gui": {
            "rotation": [0, 0, 0],
            "translation": [0, 0, 0],
            "scale": [1, 1, 1]
        },
        "fixed": {
            "rotation": [0, 0, 0],
            "translation": [0, 0, 0],
            "scale": [1, 1, 1]
        }
    }
}
```
And your item should now render the OBJ model with the proper transformations specified in its model file.

So far, only vanilla model transformations are supported by FOML.
