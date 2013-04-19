---
layout: documentation
title: cdec - External feature functions
---

External feature functions are [feature functions](/concepts/feature_functions.html) that are loaded as a dynamically linked library at run-time to extract features from derivations in a hypergraph. This permits feature functions to be implemented in other code bases without requiring `cdec` to have build dependencies on external software.

# Specifying external feature functions in your cdec.ini file
To load feature external feature functions, you can specify them in your `cdec.ini` configuration file as follows:

    feature_function=External /path/to/libmy_feature.so [extra options]

Any extra options are passed to the external library.

# Implementing external feature functions

You must implement the following function in the dynamic library containing your external feature function(s):

{% highlight c++ %}
extern "C" FeatureFunction* create_ff(const std::string& ff_and_args) {
  return new MyFeatureFunction(ff_and_args);
}
{% endhighlight %}

# Example

An example external feature function is included in `cdec`, in the [`example_extff/`](https://github.com/redpony/cdec/tree/master/example_extff) directory.

