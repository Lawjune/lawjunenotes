# Composite Pattern

```pattern
[Interface::Component] <--realize-- [Shape]
					   <--realize-- [Group]

[Component]
	+ render()

[Shape]
	+ render()

[Group]
	- vector<Component *> _cmps
	+ render()
	+ add(Component cmp)
```


```pattern_of_gof
[Interface::Component] <--realize-- [Leaf]
					   <--realize-- [Composite]

[Component]
	+ operation()

[Leaf]
	+ operation()

[Composite]
	- vector<Component *> _cmps
	+ operation()
	+ add(Component cmp)
```

https://refactoring.guru/design-patterns/composite/cpp/example

```cpp
#include <iostream>
#include <string>
#include <list>

class Component {
public:
    virtual void render() = 0;
    virtual void move() = 0;
};

class Shape : public Component {
public:
    void render() {
        std::cout << "Render Shape." << std::endl;
    }
    
    void move() {
        std::cout << "Move Shape." << std::endl;
    }
};

class Group : public Component {
private:
    std::list<Component *> _cmps;
public:
    void add(Component *cmp) {
        _cmps.push_back(cmp);
    }
    
    void render() {
        for (auto* cmp : _cmps)
            cmp->render();
    }
    
    void move() {
        for (auto* cmp : _cmps)
            cmp->move();
    }
};

int main(int argc, const char * argv[])
{
    Shape * shape_0 = new Shape();
    Shape * shape_1 = new Shape();
    Shape * shape_2 = new Shape();
    Shape * shape_3 = new Shape();
    
    Group * group_0 = new Group();
    Group * group_1 = new Group();
    
    group_0->add(shape_0);
    group_0->add(shape_1);
    group_1->add(shape_2);
    group_1->add(shape_3);
    
    group_0->render();
    group_0->move();
    
    group_1->render();
    group_1->move();
    
    delete group_1;
    delete group_0;
    delete shape_3;
    delete shape_2;
    delete shape_1;
    delete shape_0;
    
    return 0;
}
```
```output
Render Shape.
Render Shape.
Move Shape.
Move Shape.
Render Shape.
Render Shape.
Move Shape.
Move Shape.
```

# Adapter Pattern

```cpp
#include <iostream>
#include <string>
#include <list>

class Image {
    
};

class Filter {
public:
    virtual void apply(Image *image) = 0;
};

class VividFilter : Filter {
public:
    void apply(Image *image) override {
        std::cout << "Applying Vivid Filter." << std::endl;
    }
};

class ImageView {
private:
    Image * _image;
    
public:
    ImageView(Image *image) : _image(image) {}
    
    void apply(Filter *fitler) {
        fitler->apply(_image);
    }
};


int main(int argc, const char * argv[])
{
    auto* image = new Image();
    auto* image_view = new ImageView(image);
    auto* vivid_filter = new VividFilter();
    image_view->apply((Filter *)vivid_filter);
    
    delete vivid_filter;
    delete image_view;
    delete image;
    
    return 0;
}
```
```output
Applying Vivid Filter.
```

*If we want to import tens of beautiful filters from the 3rd party library. But the 3rd party `Filter` is not inherited or does not implement from the `Filter` we built.*

```pattern
[ImageView] --dependency--> [Filter]
[CaramelFilter] --inherit--> [Filter]
[CaramelFilter] --component--> [Caramel]


[ImageView]
	+ apply(filter)

[Filter]
	+ apply(photo)


[CaramelFilter] - [Adapter]
[Caramel] - [Adaptee]
```

https://refactoring.guru/design-patterns/adapter/cpp/example

```cpp
#include <iostream>
#include <string>
#include <list>

class Image {
    
};

class Filter {
public:
    virtual void apply(Image *image) = 0;
};

class VividFilter : Filter {
public:
    void apply(Image *image) override {
        std::cout << "Applying Vivid Filter." << std::endl;
    }
};

class ImageView {
private:
    Image * _image;
    
public:
    ImageView(Image *image) : _image(image) {}
    
    void apply(Filter *fitler) {
        fitler->apply(_image);
    }
};

class Caramel {
public:
    void init() {
        std::cout << "Init Caramel" << std::endl;
    }

    void render(Image *image) {
        std::cout << "Applying Caramel Filter" << std::endl;
    }
};

class CaramelFilter : Filter{
private:
    Caramel * _caramel;
    
public:
    CaramelFilter(Caramel * caramel) : _caramel(caramel) {}
    
    void apply(Image *image) override {
        _caramel->init();
        _caramel->render(image);
    }
};

int main(int argc, const char * argv[])
{
    auto* image = new Image();
    auto* image_view = new ImageView(image);
    auto* vivid_filter = new VividFilter();
    image_view->apply((Filter *)vivid_filter);
    
    auto* caramel = new Caramel();
    auto* caramel_filter = new CaramelFilter(caramel);
    image_view->apply((Filter *)caramel_filter);
    
    delete caramel_filter;
    delete caramel;
    delete vivid_filter;
    delete image_view;
    delete image;
    
    return 0;
}
```
```output
Applying Vivid Filter.
Init Caramel
Applying Caramel Filter
```

# Decorator Pattern


**The Problem**
*How to flexibly add new features?*
```cpp
#include <iostream>
#include <string>
#include <list>

class CloudStream {
public:
    virtual void write(std::string data) {
        std::cout << "Storing " << data << std::endl;
    }
};

class EncryptedCloudStream : public CloudStream {
private:
    std::string _encrypt(std::string data) {
        return "!@R%OI$U#$WE@&";
    }
    
public:
    void write(std::string data) override {
        auto encrypted = _encrypt(data);
        CloudStream::write(encrypted);
    }
};

class CompressedCloudStream : public CloudStream {
private:
    std::string _compress(std::string data) {
        return data.substr(0, 5);
    }
    
public:
    void write(std::string data) override {
        auto compressed = _compress(data);
        CloudStream::write(compressed);
    }
}

int main(int argc, const char * argv[])
{
    auto cloud_stream = new EncryptedCloudStream();
    
    cloud_stream->write("Here's some data!");
    
    delete cloud_stream;
    
    return 0;
}
```

*The problem structure:*
[CloudStream] <--inheritance-- [Encrypted]
              <--inheritance-- [Compressed]
              <--inheritance-- [EncryptedAndCompressed]

*Favor Composition Over INheritance*  

**Solution:**

[Stream](Interface) <--implement-- [CloudStream]
                    <--implement-- [Encrypted]  
                    <--composite--

[Stream]
    +write(data)

[Encrypted] implements [Stream]
    -Stream stream
    +write(data) {
        encrypted = encrypt(data);
        stream.write(encrypted);
    }


=>**Gof Presentation:**

[Component](Interface) <--implement-- [ConcreteComponent]
                       <--implement-- [Decorator]  
                       <--composite--

[Component]
    +operation() 

[Decorator] implements [Component]

    +write(data) {
        // additional behavior
        component.operation();
    }


































