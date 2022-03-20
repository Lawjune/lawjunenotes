# Mememto

```pattern
[Editor] --dependency--> [EditorState] <--composite--* [History]

[Editor] -> Orignator
	- content: string
	+ createState()
	+ restore()

[EditorState] -> Mememto
	- content: string

[History] -> Caretaker
	- state: List
	+ push(state)
	+ pop()
```

*References:*
https://refactoring.guru/design-patterns/memento/cpp/example

```cpp
#include <iostream>
#include <string>
#include <vector>

class EditorState {
private:
    const std::string _content;
    
public:
    EditorState(const std::string& str) : _content(str) {}
    std::string get_content() const { return _content;}
};

class Editor {
private:
    std::string _content;
    
public:
    
    EditorState *create_state()
    {
        return new EditorState(_content);
    }
    
    void restore(EditorState *state)
    {
        _content = state->get_content();
    }
    
    void set_content(std::string content)
    {
        _content = content;
    }
    
    std::string get_content()
    {
        return _content;
    }
};

class History {
private:
    std::vector<EditorState *> _states;
    
public:
    void push(EditorState *state)
    {
        _states.push_back(state);
    }
    
    EditorState *pop()
    {
        EditorState* last_state =  _states.back();
        _states.pop_back();
        
        return last_state;
    }
};

int main(int argc, const char * argv[])
{
    Editor editor;
    History history;
    
    editor.set_content("a");
    history.push(editor.create_state());
    editor.set_content("b");
    history.push(editor.create_state());
    editor.set_content("c");
    editor.restore(history.pop());
    std::cout << editor.get_content() << std::endl;

    return 0;
}
```
```output
b
```

***There is memory leak in above code!!!***

```cpp
#include <iostream>
#include <string>
#include <vector>

class EditorState {
private:
    const std::string _content;
    
public:
    ~EditorState() { std::cout << "EditorState Destroy" << std::endl; }
    EditorState(const std::string& str) : _content(str) {}
    std::string get_content() const { return _content;}
};

class Editor {
private:
    std::string _content;
    
public:
    
    std::shared_ptr<EditorState> create_state()
    {
        std::shared_ptr<EditorState> editor_state(new EditorState(_content));
        return editor_state;

    }
    
    void restore(std::shared_ptr<EditorState> state)
    {
        _content = state->get_content();
    }
    
    void set_content(std::string content)
    {
        _content = content;
    }
    
    std::string get_content()
    {
        return _content;
    }
};

class History {
private:
    std::vector< std::shared_ptr<EditorState> > _states;
    
public:
    void push(std::shared_ptr<EditorState> state)
    {
        _states.push_back(state);
    }
    
    std::shared_ptr<EditorState> pop()
    {
        std::shared_ptr<EditorState> last_state =  _states.back();
        _states.pop_back();
        
        return last_state;
    }
};

int main(int argc, const char * argv[])
{
    Editor editor;
    History history;
    
    editor.set_content("a");
    history.push(editor.create_state());
    editor.set_content("b");
    history.push(editor.create_state());
    editor.set_content("c");
    editor.restore(history.pop());
    std::cout << editor.get_content() << std::endl;

    return 0;
}
```
```output
EditorState Destroy
b
EditorState Destroy
```

**Exercise**
*Exercise In the Exercises project, look at the code in the memento/Document class. This class represents a document in a word processor like MS Word or Apple Pages. *

*Our Document class has three attributes:  
	-content 
	-fontName 
	-fontSize  
We should allow the user to undo the changes to any of these attributes. In the future, we may add additional attributes in this class and these attributes should also be undoable.  Implement the undo feature using the memento pattern.*

```cpp
#include <iostream>
#include <string>
#include <vector>

template<typename T>
class AttributeState {
private:
    const T _attribute;

public:
    AttributeState(const T& attr) : _attribute(attr) {}
    T get_attribute() const { return _attribute;}
};

class Document {
private:
    std::string _content;
//    std::string _font_name;
    int _font_size;

public:
    
    // content
    std::shared_ptr< AttributeState<std::string> > create_content_state()
    {
        std::shared_ptr< AttributeState<std::string> > content_state(new AttributeState<std::string>(_content));
        return  content_state;
    }
    
    void restore_content(std::shared_ptr< AttributeState<std::string> > state)
    {
        _content = state->get_attribute();
    }
    
    void set_content(std::string content)
    {
        _content = content;
    }
    
    std::string get_content()
    {
        return _content;
    }
    
    // font_size
    std::shared_ptr< AttributeState<int> > create_font_size_state()
    {
        std::shared_ptr< AttributeState<int> > font_size_state(new AttributeState<int>(_font_size));
        return  font_size_state;
    }
    
    void restore_font_size(std::shared_ptr< AttributeState<int> > state)
    {
        _font_size = state->get_attribute();
    }
    
    void set_font_size(int font_size)
    {
        _font_size = font_size;
    }
    
    int get_font_size()
    {
        return _font_size;
    }
};

template<typename T>
class History {
private:
    std::vector<T> _states;
    
public:
    void push(T state)
    {
        _states.push_back(state);
    }
    
    T pop()
    {
        T last_state = _states.back();
        _states.pop_back();
        return last_state;
    }
    
};

int main(int argc, const char * argv[])
{
    Document doc;
    History< std::shared_ptr< AttributeState<std::string> > > content_history;
    History< std::shared_ptr< AttributeState<int> > > font_size_history;
    
    doc.set_content("a");
    content_history.push(doc.create_content_state());
    doc.set_content("b");
    content_history.push(doc.create_content_state());
    doc.set_content("c");
    doc.restore_content(content_history.pop());
    std::cout << doc.get_content() << std::endl;
    
    doc.set_font_size(4);
    font_size_history.push(doc.create_font_size_state());
    doc.set_font_size(7);
    font_size_history.push(doc.create_font_size_state());
    doc.set_font_size(14);
    doc.restore_font_size(font_size_history.pop());
    std::cout << doc.get_font_size() << std::endl;

    return 0;
}
```

# State Pattern

```pattern
[Main] --dependency--> [UIControl] <--Inheritance-- [TextBox]
								   <--Inheritance-- [CheckBox]

[UIControl] -> Context
	+ draw()

[TextBox] -> State
	+ draw()

[CheckBox] -> ConcreteStateA
	+ draw()
```

```pattern
[Canvas] *--composite--> [Tool] <--Inheritance-- [Selection]
							    <--Inheritance-- [Brush]

[Canvas] -> Context
	- currentTool
	+ mouseDown()
	+ mouseUp()

[Tool] -> State
	+ mouseDown()
	+ mouseUp()

[Selection] -> ConcreteStateA
	+ mouseDown()
	+ mouseUp()

[Brush] -> ConcreteStateA
	+ mouseDown()
	+ mouseUp()
```

https://refactoring.guru/design-patterns/state/cpp/example#:~:text=State%20%2F%20C%2B%2B-,State%20in%20C%2B%2B,of%20acting%20on%20its%20own.

```cpp
#include <iostream>

class Canvas;

class Tool {
private:
    Canvas * _canvas;

public:
    Canvas * get_canvas() { return _canvas; }
    void set_convas(Canvas * canvas) {
        _canvas = canvas;
    }
    
    virtual ~Tool() {}
    
    virtual void mouse_down() = 0;
    virtual void mouse_up() = 0;
    
};

class Canvas {
private:
    Tool * _tool;

public:
    
    Canvas(Tool * tool) : _tool(nullptr) {
        set_tool(tool);
    }
    
    ~Canvas() {
        delete _tool;
    }
    
    void set_tool(Tool * tool) {
        std::cout << "Set current tool to " << typeid(*tool).name() << std::endl;
        if (_tool != nullptr)
            delete _tool;
        _tool = tool;
        _tool->set_convas(this);
    }
    
    void mouse_down() {
        _tool->mouse_down();
    }
    
    void mouse_up() {
        _tool->mouse_up();
    }
};


class Selection : public Tool {
    void mouse_down() override {
        std::cout << "Selection icon" << std::endl;
    }
    
    void mouse_up() override {
        std::cout << "Draw a dashed rectangle" << std::endl;
    }
};

class BrushTool : public Tool {
    void mouse_down() override {
        std::cout << "Brush icon" << std::endl;
    }
    
    void mouse_up() override {
        std::cout << "Draw a line" << std::endl;
    }
};

void client_code_selection() {
    Canvas * canvas = new Canvas(new Selection);
    canvas->mouse_down();
    canvas->mouse_up();
    delete canvas;
}

void client_code_brush() {
    Canvas * canvas = new Canvas(new BrushTool);
    canvas->mouse_down();
    canvas->mouse_up();
    delete canvas;
}

int main(int argc, const char * argv[])
{
    client_code_selection();
    client_code_brush();

    return 0;
}
```

***Abusing the State Pattern Example***

```cpp
#include <iostream>

class StopWatch {
private:
    bool _is_running;
    
public:
    void click() {
        if (_is_running) {
            _is_running  = false;
            std::cout << "Stopped" << std::endl;
        } else {
            _is_running = true;
            std::cout << "Running" << std::endl;
        }
    }
};

int main(int argc, const char * argv[])
{

    StopWatch * stop_watch = new StopWatch();
    
    stop_watch->click();
    
    delete stop_watch;
    return 0;
}
```

***Nightmare starts!***
```cpp
class State;

class StopState : public State;
class RunningState : public State;
```

# Strategy Pattern

```pattern
[ImageStorage] *--composite--> [Compressor] <--Inheritance-- [TextBox]
                                            <--Inheritance-- [CheckBox]

[ImageStorage] *--composite--> [Filter] <--Inheritance-- [BlackAndWhite]
                                        <--Inheritance-- [HighContrast]

[ImageStorage] -> Context
    - compressor
    - filter
    + store()

[Compressor] -> Strategy
    + compressor()
[JpegCompressor] -> ConcreteStrategyA
[PngCompressor] -> ConcreteStrategyB

[Filter] -> Strategy
    + filter()
[BlackAndWhite] -> ConcreteStrategyA
[HighContrast] -> ConcreteStrategyB
```

https://refactoring.guru/design-patterns/strategy/cpp/example


**Solution - Structed** 

```cpp
#include <iostream>
#include <string>

class Compressor {
public:
    virtual ~Compressor() {}
    virtual void compress(std::string file_name) const = 0;
};

class Filter {
public:
    virtual ~Filter() {}
    virtual void filter(std::string file_name) const = 0;
};

class ImageStorage {
private:
    Compressor * m_compressor;
    Filter * m_filter;
    
public:
    ImageStorage(Compressor * compressor = nullptr,
                 Filter * filter = nullptr) :
        m_compressor(compressor), m_filter(filter) {}
    
    ~ImageStorage() {
        delete m_compressor;
        delete m_filter;
    }
    
    void store(std::string file_name) {
        m_compressor->compress(file_name);
        m_filter->filter(file_name);
        
    }
    
    void set_compressor(Compressor * compressor) {
        delete m_compressor;
        m_compressor = compressor;
    }
    
    void set_filter(Filter * filter) {
        delete m_filter;
        m_filter = filter;
    }
};

class JpegCompressor : public Compressor {
public:
    void compress(std::string file_name) const override {
        std::cout << "Compressing using JPEG" << std::endl;
    }
};

class PngCompressor : public Compressor {
public:
    void compress(std::string file_name) const override {
        std::cout << "Compressing using PNG" << std::endl;
    }
};

class BlackAndWhiteFilter : public Filter {
public:
    void filter(std::string file_name) const override {
        std::cout << "Applying Black and White filter" << std::endl;
    }
};

class HighContrast : public Filter {
public:
    void filter(std::string file_name) const override {
        std::cout << "Applying High Contrast filter" << std::endl;
    }
};

int main(int argc, const char * argv[])
{
    ImageStorage * image_storage = new ImageStorage(new JpegCompressor,
                                                  new BlackAndWhiteFilter);
    
    image_storage->store("a");
    
    std::cout << "Now change the strategies..." << std::endl;
    image_storage->set_compressor(new PngCompressor);
    image_storage->set_filter(new HighContrast);
    
    image_storage->store("a");
    
    delete image_storage;
    return 0;
}
```
```output
Compressing using JPEG
Applying Black and White filter
Now change the strategies...
Compressing using PNG
Applying High Contrast filter
```

**Solution - Flying**
```cpp
#include <iostream>
#include <string>

class Compressor {
public:
    virtual ~Compressor() {}
    virtual void compress(std::string file_name) const = 0;
};

class Filter {
public:
    virtual ~Filter() {}
    virtual void filter(std::string file_name) const = 0;
};

class ImageStorage {
    
public:
    
    void store(std::string file_name,
               Compressor * compressor,
               Filter * filter) {
        compressor->compress(file_name);
        filter->filter(file_name);
    }
};

class JpegCompressor : public Compressor {
public:
    void compress(std::string file_name) const override {
        std::cout << "Compressing using JPEG" << std::endl;
    }
};

class PngCompressor : public Compressor {
public:
    void compress(std::string file_name) const override {
        std::cout << "Compressing using PNG" << std::endl;
    }
};

class BlackAndWhiteFilter : public Filter {
public:
    void filter(std::string file_name) const override {
        std::cout << "Applying Black and White filter" << std::endl;
    }
};

class HighContrastFilter : public Filter {
public:
    void filter(std::string file_name) const override {
        std::cout << "Applying High Contrast filter" << std::endl;
    }
};

int main(int argc, const char * argv[])
{
    ImageStorage * image_storage = new ImageStorage();
    JpegCompressor * jpeg_compressor = new JpegCompressor();
    PngCompressor * png_compressor = new PngCompressor();
    BlackAndWhiteFilter * black_and_white_filter = new BlackAndWhiteFilter();
    HighContrastFilter * high_constrast_filter = new HighContrastFilter();
    
    image_storage->store("a", jpeg_compressor, black_and_white_filter);
    std::cout << "Now change to new strategies..." << std::endl;
    image_storage->store("a", png_compressor, high_constrast_filter);
    
    delete image_storage;
    delete jpeg_compressor;
    delete black_and_white_filter;
    delete high_constrast_filter;
    return 0;
}
```
```output
Compressing using JPEG
Applying Black and White filter
Now change the strategies...
Compressing using PNG
Applying High Contrast filter
```

# Command Pattern

```pattern
[Button] *--composite--> [Command] <--dependency-- [AddCustomer] --dependency--> [CustomerService]


-------FRAMEWORK-------
[Button] -> Invoker
    + click()

[Command] 
    + execute()
-------FRAMEWORK-------


----------APP----------
[CustomerService] -> ConcreteCommand
    + addCustomer()

[AddCustomer] -> Receiver
    + execute()
----------APP----------
```

**Decouple the Invoker(Sender) with the Receiver.**

https://refactoring.guru/design-patterns/command/cpp/example#:~:text=Command%20%2F%20C%2B%2B-,Command%20in%20C%2B%2B,%2C%20storing%20command%20history%2C%20etc.

```cpp
#include <iostream>
#include <string>

class Command {
public:
    virtual ~Command() {}
    
    virtual void execute() const = 0;
};

class Button {
private:
    std::string label;
    Command * m_command;
    
public:
    ~Button() {
        delete m_command;
    }
    
    Button(Command * command=nullptr) : m_command(command) {}
    
    void click() {
        m_command->execute();
    }
};

class CustomerService {
public:
    void add_customer() {
        std::cout << "Add customer" << std::endl;
    }
};

class AddCustomerCommand : public Command {
private:
    CustomerService * m_service;
    
public:
    ~AddCustomerCommand() {
        delete m_service;
    }
    
    AddCustomerCommand(CustomerService * service=nullptr) : m_service(service) {}
    
    void execute() const override {
        m_service->add_customer();
    }
};

int main(int argc, const char * argv[])
{
    auto * button = new Button(new AddCustomerCommand(new CustomerService));
    
    button->click();
    
    delete button;
    
    return 0;
}
```
```output
Add customer
```

**Composite Command**
```cpp
class Command {
public:
    virtual ~Command() {}
    
    virtual void execute() const = 0;
};

class ResizeCommand : public Command {
public:
    void execute() const override {
        std::cout << "Resize" << std::endl;
    }
};

class BlackAndWhiteCommand : public Command {
    void execute() const override {
        std::cout << "Black and white" << std::endl;
    }
};

class CompositeCommand : public Command {
private:
    std::vector<Command *> m_commands;
    
public:
    ~CompositeCommand() {
        for (auto cmd : m_commands) {
            delete cmd;
        }
    }
    
    void add(Command * command) {
        m_commands.push_back(command);
    }
    
    void execute() const override {
        for (auto cmd : m_commands) {
            cmd->execute();
        }
    }
};

int main(int argc, const char * argv[])
{
    auto composite = new CompositeCommand();
    
    composite->add(new ResizeCommand);
    composite->add(new BlackAndWhiteCommand);
    
    composite->execute();
    
    delete composite;
    
    return 0;
}
```

**Undoable Commands**

```pattern
[Command] <--inheritance-- [UndoableCommand] <--Inheritance-- [BoldCommand]

[UndoableCommand]
    + unexecute()

[BoldCommand]
    - m_pre_content: string
    + execute()
    + unexecute()

[BoldCommand] *--composite--> [Document]
[BoldCommand] *--composite--> [History]
[UndoCommand] *--composite--> [History]

[Document]
    + make_bold()

BoldCommand.execute() {
    m_pre_content = doc.get_content();
    document.make_bold();
    history.push(this);
}

BoldCommand.unexecute() {
    doc.set_content(m_pre_content);
}

UndoCommand.execute() {
    last = history.pop();
    last.unexecute();
}
```

```cpp
#include <iostream>
#include <string>
#include <vector>

class Command {
public:
    virtual ~Command() {}
    
    virtual void execute() const = 0;
};

class UndoableCommand : public Command {
public:
    virtual void unexecute() const = 0;
};

class History {
private:
    std::vector<UndoableCommand *> m_commands;

public:
    ~History() {
        for (auto cmd : m_commands) {
            delete cmd;
        }
    }
    
    void push(UndoableCommand * command) {
        m_commands.push_back(command);
    }
    
    UndoableCommand * pop() {
        auto last = m_commands.back();
        m_commands.pop_back();
        return last;
    }
    
    int size() {
        return (int)m_commands.size();
    }
};

class UndoCommand : public Command {
private:
    History * m_history;
    
public:
    UndoCommand(History * history=nullptr) : m_history(history) {}
    
    void execute() const override {
        std::cout << "history size: " << m_history->size() << std::endl;
        if (m_history->size() > 0) {
            m_history->pop()->unexecute();
        }
    }
    
};

class HtmlDocument {
private:
    std::string m_content;
    
public:
    void make_bold() {
        m_content = "<b>" + m_content + "</b>";
    }
    
    std::string get_content() {
        return m_content;
    }
    
    void set_content(std::string content) {
        m_content = content;
    }
};

class BoldCommand : public UndoableCommand {
    
private:
    mutable std::string m_prev_content;
    HtmlDocument * m_html_doc;
    History * m_history;
public:
    
    ~BoldCommand() {
        delete m_html_doc;
//        delete m_history;
    }
    
    BoldCommand(HtmlDocument * html_doc=nullptr, History * history=nullptr) :
        m_html_doc(html_doc), m_history(history) {}
    
    void set_prev_content(std::string content) {
        m_prev_content = content;
    }

    void execute() const override {
        m_prev_content = m_html_doc->get_content();
        
        m_html_doc->make_bold();
        m_history->push((UndoableCommand *)this);
    }
    
    void unexecute() const override {
        m_html_doc->set_content(m_prev_content);
    }
};

int main(int argc, const char * argv[])
{
    auto * history = new History();
    auto * html_document = new HtmlDocument();
    
    html_document->set_content("Hello World!");
    
    auto * bold_command = new BoldCommand(html_document, history);
    bold_command->execute();
    std::cout << html_document->get_content() << std::endl;

    bold_command->unexecute();
    std::cout << html_document->get_content() << std::endl;
    
    delete history;
    
    return 0;
}
```
```output
<b>Hello World!</b>
Hello World!
```

# Iterator Pattern

***Before Applied Patter***
```pattern
[BrowserHistory]
    - url: string
    + push(url)
    + pop()
    + next()
    + current()
    + has_next()
```

```cpp
while (history->has_next()) {
    auto current = history->current();
    // Do something
    history->next();
}
```

***Applied Pattern***
```Iterator
[BrowserHistory] 

[Iterator] <--Inheritance-- [VectorIterator]
           <--Inheritance-- [AraryIterator]

[BrowserHistory]
    - url: string
    + push(url)
    + pop()

[Iterator]
    + next()
    + current()
    + has_next()
```

https://refactoring.guru/design-patterns/iterator/cpp/example


```cpp
#include <iostream>
#include <string>
#include <vector>

class Iterator {
public:
    virtual ~Iterator() {}
    virtual bool has_next() const = 0;
    virtual std::string current() const = 0;
    virtual void next() = 0;
};

class BrowserHistory {
private:
    std::vector<std::string> _urls;

public:
    std::string pop() {
        auto url = _urls.back();
        _urls.pop_back();
        return url;
    }
    
    void push(std::string url) {
        _urls.push_back(url);
    }
    
    std::vector<std::string> * get_urls() {
        return &_urls;
    }
    
    Iterator * create_iterator() {
        return new VectorIterator(this);
    }
    
    class VectorIterator : public Iterator {
    private:
        BrowserHistory * _history;
        int _index;
    public:
        VectorIterator(BrowserHistory * history) : _history(history) {}
        
        bool has_next() const override {
            return _index < _history->get_urls()->size();
        }
        
        std::string current() const override {
            return _history->get_urls()->at(_index);
        }
        
        void next() override {
            _index--;
        }
    };
};


int main(int argc, const char * argv[])
{
    auto * history = new BrowserHistory();
    history->push("a");
    history->push("b");
    history->push("c");
    
    Iterator * iterator = history->create_iterator();
    
    while (iterator->has_next()) {
        auto url = iterator->current();
        std::cout << "Crruent URL: " << url << std::endl;
        iterator->next();
    }
    
    delete history;
    delete iterator;
    
    return 0;
}
```

***Benefits: Easy to change vector to array***

```cpp
#include <iostream>
#include <string>
#include <vector>

class Iterator {
public:
    virtual ~Iterator() {}
    virtual bool has_next() const = 0;
    virtual std::string current() const = 0;
    virtual void next() const = 0;
};  

class BrowserHistory {
private:
    std::string * _urls = new std::string[10];
    int _count = 0;

public:
    ~BrowserHistory() {
        delete[] _urls;
    }
    
    std::string pop() {
        _count--;
        return _urls[--_count];
    }
    
    void push(std::string url) {
        _urls[_count++] = url;
    }
    
    std::string * get_urls() {
        return _urls;
    }
    
    Iterator * create_iterator() {
        return new ArrayIterator(this);
    }
    
    class ArrayIterator : public Iterator {
        
    private:
        BrowserHistory * _history;
        mutable int _index;
    public:
        ArrayIterator(BrowserHistory * history) : _history(history) {}
        
        bool has_next() const override {
            return (_index < _history->_count);
        }
        
        std::string current() const override {
            return _history->get_urls()[_index];
        }
        
        void next() const override {
            _index++;
        }
    };
    
};


int main(int argc, const char * argv[])
{
    auto * history = new BrowserHistory();
    history->push("a");
    history->push("b");
    history->push("c");
    
    Iterator * iterator = history->create_iterator();
    
    while (iterator->has_next()) {
        auto url = iterator->current();
        std::cout << "Crruent URL: " << url << std::endl;
        iterator->next();
    }
    
    delete history;
    delete iterator;
    
    return 0;
}
```

# Template Method Pattern


**To Fix the Problems of Strategy Pattern**
```pattern
[TaskExecutor] *--composite--> [Task] <--Inheritance-- [TransferMoney]
                                      <--Inheritance-- [GenerateReport]

[TaskExecutor]
    - AuditTrial * _audit_trial
    + execute(Task * task)

[Task]
    + execute() // Contains the common part => *_audit_trial->record
    + do_execute() // To combine the execute()

[TransferMoney] : [Task]
    + do_execute()

[GenerateReport] : [Task]
    + do_execute()
```

```pattern - GOF
[AbstractClass]
    + template_method() 
    + primitive_operation_1()
    + primitive_operation_2()

[ConcreteClass] : [AbstractClass]
    + primitive_operation_1()
    + primitive_operation_2()
```

https://refactoring.guru/design-patterns/template-method/cpp/example

```cpp
#include <iostream>
#include <string>

class AuditTrail {
public:
    void record() {
        std::cout << "Audit" << std::endl;
    }
};

class Task {
 
private:
    AuditTrail * _audit_trail;
    
public:
    Task() : _audit_trail(new AuditTrail) {} ;
    Task(AuditTrail * audit_trail) : _audit_trail(audit_trail) {}
    ~Task() {
        delete _audit_trail;
    }
    
    void execute() {
        _audit_trail->record();
        do_execute();
    }
    
protected:
    virtual void do_execute() const = 0;
};

class TransferMoneyTask : public Task {
protected:
    void do_execute() const override {
        std::cout << "Transfer Money" << std::endl;
    }
};

class GenerateReportTask : public Task {
protected:
    void do_execute() const override {
        std::cout << "Generate Report" << std::endl;
    }
};

int main(int argc, const char * argv[])
{
    Task * transfer_money_task = new TransferMoneyTask();
    transfer_money_task->execute();
    return 0;
}
```


# Observer Pattern

```pattern
[DataSource] *--composite--> [Observer] <--Inheritance-- [Spreadsheet]
                                        <--Inheritance-- [Chat]

[DataSource]
    - value
    + get_value()
    + set_value()

    + add_observer(obs)
    + remove_observer(obs)
    + notity_observer()


[Observer]
    + update()
```

```patter GOF
[Subject] *--composite--> [Observer] <--Inheritance-- [ConcreteObserverA]
                                     <--Inheritance-- [ConcreteObserverB]                                     

[Subject]
    + attach(obs)
    + detach(obs)
    + notify()

[ConcreteSubject] : [Subject]


[Observer]
    + update()
```

https://refactoring.guru/design-patterns/observer/cpp/example#:~:text=Observer%20%2F%20C%2B%2B-,Observer%20in%20C%2B%2B,that%20implements%20a%20subscriber%20interface.3


```cpp
#include <iostream>
#include <string>
#include <list>

class Observer {
public:
    virtual ~Observer() {};
    virtual void update() const = 0;
};


class Subject {
private:
    std::list<Observer * > _observers;
    
public:
    virtual ~Subject() {}
    
    
    void add_observer(Observer * observer) {
        _observers.push_back(observer);
    }
    
    void remove_observer(Observer * observer) {
        _observers.remove(observer);
    }
    
    void nofity_observers() {
        std::list<Observer * >::iterator iterator = _observers.begin();
        while (iterator != _observers.end()) {
            (*iterator)->update();
            ++iterator;
        }
    }
    
};

class DataSource : public Subject {
private:
    int _value;
    
public:
    int get_value() {
        return _value;
    }
    
    void set_value(int value) {
        _value = value;
        nofity_observers();
    }
};

class Chart : public Observer {
public:
    void update() const override {
        std::cout << "Chart got updated." << std::endl;
    }
};

class SpreadSheet : public Observer {
public:
    void update() const override {
        std::cout << "SpreadSheet got updated." << std::endl;
    }
};

int main(int argc, const char * argv[])
{
    
    DataSource * data_source = new DataSource();
    SpreadSheet * sp_0 = new SpreadSheet();
    SpreadSheet * sp_1 = new SpreadSheet();
    Chart * chart = new Chart();
    
    data_source->add_observer(sp_0);
    data_source->add_observer(sp_1);
    data_source->add_observer(chart);
    
    data_source->set_value(7);
    
    delete data_source;
    delete sp_0;
    delete sp_1;
    delete chart;

    return 0;
}
```output
SpreadSheet got updated.
SpreadSheet got updated.
Chart got updated.
```


**PUSH STYLE**
```patter 
[Subject] *--composite--> [Observer] <--Inheritance-- [ConcreteObserver]
                                

[Subject] <--dependency-- [ConcreteSubject] 

[Observer]
    - update(value)         
```

**PULL STYLE**
```patter 
[Subject] *--composite--> [Observer] <--Inheritance-- [ConcreteObserver]
                                

[Subject] <--dependency-- [ConcreteSubject] *--composite--> [ConcreteObserver]      

[ConcreteSubject]
    + get_value()
```

# Mediator Pattern

```pattern
[ListBox] --dependency--> [DialogBox] <--dependency-- [TextBox]
                          [DialogBox] <--dependency-- [Button]

[DialogBox] <--inheritance-- [ArticlesDialogBox]

[DialogBox]
    + change(control)                         
```


```pattern - GOF
[Colleague] --dependency--> [Mediator] 

[Mediator] <--inheritance-- [ConcreteMediator] --dependency--> [ConcreteColleague]                        
```





















































