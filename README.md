# Kludge Guru style guide

This is arbitrary but consistent, or at least I find it consistent. I expect you to follow these a bit non-obvious but useful rules when working in a project I lead.

## Indentation and line breaks

All manually edited files are indented with **Tab** character. The indentation level is always one tab, there is no "continuation indent". Exception is this Markdown document which uses spaces for technical reasons.

**All** things start and end on the **same** indentation level. Indentation level is always incremented by **one** tab.

Do this:

    abc({
        def(1, 2, 3),
        ghi
    });
    
**Don't** end block on a different level:

    abc({
        def(1, 2, 3),
        ghi
        }); // wrong
        
**Don't** add extra tabs:

    abc({
            def(1, 2, 3), // wrong
            ghi
    });
    
Same indentation *level* does **not** mean same character position. **Don't** break the line before parentheses, braces, etc.

    if (a)
    { // wrong
        ...
    }
        
Valid TSX example:

    <abc>
        <def>{ghi}</def>
        <el
            attr="val"
        />
    </abc>
    
Try to keep the lines to **140** characters or less (assuming 4-character tabs).

When dealing with arrays, objects, long parameters **either** write it **all** in one line **or** break it **all** into separate lines, with beginning and end on separate lines. When splitting into lines add a trailing comma if syntax allows it (TypeScript allows trailing comma in function calls).

Do this:

    abc(d, [e, f], g);
    abc(
        d,
        [e, f],
        g,
    );
    abc(d, [
        e,
        f
    ], g);
    
The advantage of this approach is that you can always easily skip large blocks of irrelevant text just by matching up beginning and the end (e.g. in the last example you know there is exactly one parameter between `d` and `g` which starts with `[` and ends with `]` and you can skip the rest).

**Don't** break up some, but not all of list items:

    abc(
        d, e, f,
        g, h, i,
    );
    
**Don't** keep the first parameter on the same line. Treat "parameter list" as a *thing* as well — it must start and end on the same indentation level:
    
    abc(d,
        e,
        f);

If breaking up chained methods, do it immediately:

    abc()
        .def()
        .xyz();
    
**Dont't** break at some random point:

    abc().def()
        .xyz();
        
When breaking line on an operator

* Make sure all operands are on the same indentation level. Add parentheses if necessary.
* Write the operator at the start of the second line, not at the end of the first.

For example:

    if (
        a
        && b
        && (
            c
            || d
        )
    ) { ... }
    


## Whitespace

**Don't** "align" things with whitespace:

    obj = {
        longKey: value,
        also:    value,
    }

If splitting up longer functions/lists into blocks with blank lines (as you should), also add a blank space at the beginning and the end.

    function abc() {
    
        def();
        ghi();
        
        xyz();
    
    }

## Naming and structure

Type and class names are PascalCase. Types and class names are **nouns**. If you need to make a type for a verb, make a noun from it (e.g. Controller).

Functions, methods and variables are camelCase, including global variables and "constants".

Functions and methods must **start** with **verbs**: `Entity.get()` but `getEntity()`, never `entityGet()`. An exception is a qualifier for the verb/method: `maybeSubmitOrder()` or `throttledSave = throttle(save)`.

Filenames should be lower kebab-case where possible. Don't think too much about directory structure as the whole code should be navigable without relying on it.

