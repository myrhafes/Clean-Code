# **Chapter 10: Classes**

To have clean code, you should have clean classes.

## Class Organisation:
- First part: Static variables
    - public static variables.
    - private static variables.
- Second part: Local variable
    - public variables.
    - private variables.
- Third part: Function
    - public functions.
    - private functions.

### Encapsulation:
> We like to keep our variables and utility functions private, but we’re not fanatic about it. Sometimes we need to make a variable or utility function protected so that it can be accessed by a test. For us, tests rule. If a test in the same package needs to call a function or access a variable, we’ll make it protected or package scope. However, we’ll first look for a way to maintain privacy. Loosening encapsulation is always a last resort.

## Class Should Be Small:
- The first rule is that classes should be made small. The seconde principe, the class should be made smaller(The same like function).
- The class name should describe the responsibility of what it responds to. In fact, naming is probably the first way to determine the size of a class.
```java
    public class SuperDashboard extends JFrame implements MetaDataUser {
        public String getCustomizerLanguagePath() 
        public void setSystemConfigPath(String systemConfigPath) 
        public String getSystemConfigDocument() 
        public void setSystemConfigDocument(String systemConfigDocument) 
        public boolean getGuruState() 
        public boolean getNoviceState() 
        public boolean getOpenSourceState() 
        public void showObject(MetaObject object) 
        public void showProgress(String s)
        public boolean isMetadataDirty() 
        public void setIsMetadataDirty(boolean isMetadataDirty) 
        public Component getLastFocusedComponent() 
        public void setLastFocused(Component lastFocused) 
        public void setMouseSelectState(boolean isMouseSelected)
        public boolean isMouseSelected() 
        public LanguageManager getLanguageManager() 
        public Project getProject() 
        public Project getFirstProject() 
        public Project getLastProject() 
        public String getNewProjectName()
        public void setComponentSizes(Dimension dim)
        public String getCurrentDir() 
        public void setCurrentDir(String newDir) 
        public void updateStatus(int dotPos, int markPos) 
        public Class[] getDataBaseClasses() 
        public MetadataFeeder getMetadataFeeder() 
        public void addProject(Project project)
        public boolean setCurrentProject(Project project)
        public boolean removeProject(Project project) 
        public MetaProjectHeader getProgramMetadata()
        public void resetDashboard()
        public Project loadProject(String fileName, String projectName)
        public void setCanSaveMetadata(boolean canSave)
        public MetaObject getSelectedObject() 
        public void deselectObjects() 
        public void setProject(Project project) 
        public void editorAction(String actionName, ActionEvent event)
        public void setMode(int mode) 
        public FileManager getFileManager() 
        public void setFileManager(FileManager fileManager) 
        public ConfigManager getConfigManager() 
        public void setConfigManager(ConfigManager configManager) 
        public ClassLoader getClassLoader() 
        public void setClassLoader(ClassLoader classLoader) 
        public Properties getProps() 
        public String getUserHome() 
        public String getBaseDir() 
        public int getMajorVersionNumber() 
        public int getMinorVersionNumber() 
        public int getBuildNumber() 
        public MetaObject pasting(MetaObject target, MetaObject pasted, MetaProject project)
        public void processMenuItems(MetaObject metaObject)
        public void processMenuSeparators(MetaObject metaObject)
        public void processTabPages(MetaObject metaObject)
        public void processPlacement(MetaObject object) 
        public void processCreateLayout(MetaObject object) 
        public void updateDisplayLayer(MetaObject object, int layerIndex)
        public void propertyEditedRepaint(MetaObject object) 
        public void processDeleteObject(MetaObject object) 
        public boolean getAttachedToDesigner() 
        public void processProjectChangedState(boolean hasProjectChanged)
        public void processObjectNameChanged(MetaObject object) 
        public void runProject() 
        public void setAçowDragging(boolean allowDragging) 
        public boolean allowDragging() 
        public boolean isCustomizing() 
        public void setTitle(String title) 
        public IdeMenuBar getIdeMenuBar() 
        public void showHelper(MetaObject metaObject, String propertyName)
        // ... many non-public methods follow ...
    }
```

**Better:**(Small & Single Responsibility)
```java
    public class SuperDashboard extends JFrame implements MetaDataUser {
        public Component getLastFocusedComponent() 
        public void setLastFocused(Component lastFocused) 
        public int getMajorVersionNumber() 
        public int getMinorVersionNumber() 
        public int getBuildNumber() 
    }
```

### The single responsibility principle:
A class or module should have one and only one reason to change. This principle gives us a definition of responsibility and also advocates the size of the class. Class should have a responsibility - a unique reason to change.
```java
    public class Version {
        public int getMajorVersionNumber() {}
        public int getMinorVersionNumber() {}
        public int getBuildNumber() {}
    }
```

### Cohesion:
- Class should have a small number of variables. 
- Each method of a class should manipulate one or more variables.
- Each variable in the class used by each method should have maximum cohesion.
```java
public class Stack {
    private int topOfStack = 0;
    List<Integer> elements = new LinkedList<Integer>();

    public int size() {
        return topOfStack;
    }

    public void push(int element) {
        topOfStack++;
        elements.add(element);
    }

    public int pop() throws PoppedWhenEmpty {
        if (topOfStack == 0)
        throw new PoppedWhenEmpty();
        int element = elements.get(--topOfStack);
        elements.remove(topOfStack);
        return element;
    }
}
```

### Maintaining cohesion results in many small classes:
If you lose cohesion between variable and function, create new classes.

## Organizing for change:
For every system, the change is continuous. Each change leads to risk of the rest of the system no longer working as intended. In a clean system, we organize classes to reduce the risk of change.