# gloo_sample_code

Sample code for the gloo programming language.

See the gloo interpreter project here: [gloo](https://github.com/ecrane/gloo)


## Run

If you have gloo installed, you can run the examples like this:

```bash
gloo full/path/to/hello_world.gloo
```

If you set the "project_path" in the gloo config file, you can run the examples like this:

```bash
gloo hello_world
```

The .gloo extension is optional when using the project_path.


## Just Sample Code

The code in this repository is for demonstration purposes only.
As the gloo language is changing, some of the sample code might be out of date.
Use at your own risk.


## Suggested Order

 - Start with Verbs
   - show
   - put
   - tell
   - run
   - then others as needed
 - Explore Objects
   - object
   - string
   - container
   - script
   - then others as needed
 - Use lang (gloo language) for gloo concepts and syntax
 - And once you have a sense of how gloo works, explore the more advanced features and core libraries
 - For a complete example, check out the contacts app in core_libraries/web/contacts