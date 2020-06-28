# Structured Commenting
 A specification of my structured commenting scheme

Most existing commenting techniques work adiquatly when notating a few code lines but become unclear or in need of interpretation when used on large structured code segments. To signify that a comment is talking about multiple lines of code, most programmers typically block multiple lines of code under that comment without spacing between them, or leave their comment right before structural code block such as a function or loop in order to describe that structure as a whole. But what if you need to describe both a structure and it's sub components, and what if those sub components have sub components of their own? This is where this structured commenting scheme can help.

## Two types of comments
To indicate that a comment is only describing the line directly below it, 

```c++
#This comment only talks about the line directly below it
int foo = 0

int bar = 1
```

To indicate that a comment is describing multiple lines.
```c++
string alice = "Hello "
string bob = "World!"

//this comment describes the next 4 lines
    int a = 2
    int b = 3
    //this comment only talks about the line directly below it
    int c = a + b

int foo = bar
```

## Usage
Nesting comments talking about multiplel lines. Each instance of ``...`` would be replaced by the appropriate code segment.
```c++
//make pizza
    //walk to kitchen
        //face twords kitchen
            ...
        //steppy step step
            ...
    //shape dough into circle
        ...
    //add sauce
        //grab ladle
            ...
        //dunk ladle in sauce
            ...
        //place ladle over pizza
            ...
        //tilt ladle back 90 degrees
            ...
    //add cheese
        //pick up cheese
            ...
        //sprinkle cheese over pizza
            ...
    //bake
        //pick up pizza
            ...
        //walk to oven
            ...
        //place in oven
            ...
    //cut
        //grab pizza cutter
            ...
        //loop x4
            ...
            //cut pizza vertically
                ...
            //rotate pizza 12.5 degrees
                ...
```

An example of both comment types in use together
```c++
//graphics controller
    for(uint8_t i = 0; i < 9; i++){

        //where do you want to write data
        graphicsControllerIndexPort.Write(i);

        //what do you want to write there
        graphicsControllerDataPort.Write(*(registers++));
    }

//attributeController
    for(uint8_t i = 0; i < 21; i++){

        //must reset attributeController before sending data
        attributeControllerResetPort.Read();

        //where do you want to write data
        attributeControllerIndexPort.Write(i);

        //what do you want to write there
        attributeControllerWritePort.Write(*(registers++));
    }
    attributeControllerResetPort.Read();
    attributeControllerIndexPort.Write(0x20);
```

## Benefits
- readability
- code folding
- Is or can be made compatable with code formatters
## Downsides
- Does not easilly work with structurally encorced languages (such as python)
