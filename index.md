# The Quiet Brilliance of Hemanth

Say what you will about Mr. Murthy, but nothing substantial happens without hard work. He was also right about the importance of mastering English—not the performative kind acquired in fancy schools while aping Western liberal culture, but the real thing: robust vocabulary paired with solid grammar and composition skills.

My entire MCA class mocked my college buddy Hemanth as arrogant, dismissing him as an English show-off. I confess, I felt the same way then. But years later, looking back at his C code editor, I see something different entirely: sheer elegance, crystalline clarity of intent, and a rich use of metaphors in his file names and method names—Menu, Window, fillMirror, flushMirror. All of this running on MS-DOS, an operating system most considered fit only for dimwits.

## The Architecture of Thought

Consider how Hemanth structured the heart of his text editor. While we were wrestling with crude variable names and convoluted logic, he crafted something that read like poetry:

```c
typedef struct {
    char filename[MAX_FILENAME];
    char **lines;           /* Array of pointers to line strings */
    int line_count;         /* Number of lines in file */
    int current_line;       /* Current line being edited */
    int current_col;        /* Current column position */
    int modified;           /* Flag to track if file has been modified */
    char mirror[MIRROR_SIZE + 1];  /* Current line being edited */
} FileBuffer;
```

Look at that structure. `FileBuffer`—not `file_data` or `text_struct` like the rest of us would have named it. A *buffer* that holds files. The metaphor is perfect: a container that temporarily holds something precious before it moves elsewhere. And that `mirror` field—255 characters that hold "the text the user is currently editing." 

None of it would have been possible without his command of English and his unwavering work ethic.

## The Mirror Metaphor

His most brilliant insight was the mirror system. While we thought in terms of arrays and pointers, Hemanth thought in terms of reflection and truth:

```c
/* Fill mirror buffer with current line data */
void fillMirror(FileBuffer *fb) {
    int line_len;
    
    if (!fb) return;
    
    /* Clear mirror first */
    fb->mirror[0] = '\0';
    
    /* If current line exists, copy it to mirror */
    if (fb->current_line >= 0 && fb->current_line < fb->line_count && 
        fb->lines[fb->current_line]) {
        strncpy(fb->mirror, fb->lines[fb->current_line], MIRROR_SIZE);
        fb->mirror[MIRROR_SIZE] = '\0';
    }
}
```

*Fill* the mirror. Not "copy to buffer" or "load current line." Fill—like filling a vessel with water, or a mind with knowledge. The mirror reflects the current reality of the line being edited.

And then, when the user moves to a new line:

```c
/* Flush mirror buffer back to file data */
void flushMirror(FileBuffer *fb) {
    int mirror_len;
    
    if (!fb) return;
    
    /* Ensure we have enough space for lines */
    if (!growLinesArray(fb)) return;
    
    /* Allocate new memory for the line and copy from mirror */
    mirror_len = strlen(fb->mirror);
    fb->lines[fb->current_line] = (char*)malloc(mirror_len + 1);
    if (fb->lines[fb->current_line]) {
        strcpy(fb->lines[fb->current_line], fb->mirror);
        fb->modified = 1;  /* Mark file as modified */
    }
}
```

*Flush* the mirror. Like a photographer developing film, the temporary reflection becomes permanent reality. The mirror's contents flow back into the file structure, and the `modified` flag acknowledges that truth has changed.

## Precision Disguised as Arrogance

I remember he shaved his head because hair fall was becoming a distraction. He told me his productivity increased by 100% afterward. That's the kind of person he was—someone who understood that excellence requires eliminating even the smallest friction between thought and execution.

This philosophy permeated his code. Notice how he handled the transition between lines:

```c
/* Move to a different line (calls flush/fill automatically) */
void moveToLine(FileBuffer *fb, int new_line) {
    if (!fb || new_line < 0) return;
    
    /* Flush current mirror content */
    flushMirror(fb);
    
    /* Update current line */
    fb->current_line = new_line;
    fb->current_col = 0;
    
    /* Fill mirror with new line content */
    fillMirror(fb);
}
```

No friction. No confusion about state. One function call that handles the entire conceptual operation: "I want to edit a different line." The implementation handles flushing the old, updating position, and filling with the new. Seamless.

What we mistook for arrogance was actually precision. What we heard as showing off was simply a mind that thought in metaphors and abstractions, not just syntax. His English wasn't ornamental; it was operational. It gave him the vocabulary of ideas that transformed functional code into something approaching art.

## The Language of Code

While we named functions `save_file()` and `load_data()`, Hemanth wrote:

```c
int hasUnsavedChanges(FileBuffer *fb) {
    if (!fb) return 0;
    return fb->modified;
}
```

*Has* unsaved changes. A question posed to the code, as natural as asking "Does this file need saving?" His functions read like conversations with the computer, not commands barked at it.

Even his file operations carried this linguistic elegance:

```c
/* Create backup before saving */
if (createBackup(fb)) {
    printf("Backup created: %s.BAK\n", fb->filename);
}

/* Save file */
if (saveFile(fb)) {
    printf("File saved successfully.\n");
} else {
    printf("Error saving file!\n");
}
```

*Create* backup. *Save* file. Verbs that describe intention, not implementation. The code tells a story of what happens, not how it happens.

## Looking Back

In retrospect, while we were focused on the surface performance of his fluency, Hemanth was using language as a tool for clearer thinking and better work. The difference showed in everything he touched.

His text editor wasn't just functional—it was literate. Each function name was chosen with the precision of a poet selecting the perfect word. The `mirror` metaphor wasn't just clever; it was *correct*. It captured exactly what that buffer did: it reflected the current state of editing, allowing changes to be made to the reflection before committing them to reality.

We saw showing off. He was showing us the way.

The quiet brilliance wasn't in his English vocabulary—it was in understanding that code, like language, is ultimately about communication. Communication with the computer, yes, but more importantly, communication with the future programmer who would read and maintain that code.

That future programmer, as it turned out, was often himself. And sometimes, years later, it was us—finally mature enough to appreciate what we had dismissed as arrogance in our youth.
