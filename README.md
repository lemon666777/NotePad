# NotePad
This is an AndroidStudio rebuild of google SDK sample NotePad
# Notepad
---

***本实验基于NotePad应用做功能扩展***
=========================

 - 基本要求：
---------------
 -  NoteList中显示条目增加时间戳显示
 - 添加笔记查询功能（根据标题查询）
 - 附加功能：
--------
 - UI美化
 - 笔记排序

功能实现部分
======

基本要求
--

NoteList中显示条目增加时间戳显示


----------


> 时间戳显示当时日期与时间

![](https://i.imgur.com/4MihK2z.png)

> 在原有部分添加时间戳

    private static final String[] READ_NOTE_PROJECTION = new String[] {
            NotePad.Notes._ID,               // Projection position 0, the note's id
            NotePad.Notes.COLUMN_NAME_NOTE,  // Projection position 1, the note's content
            NotePad.Notes.COLUMN_NAME_TITLE, // Projection position 2, the note's title
    };
    

> 添加笔记查询功能（根据标题查询）

![](https://i.imgur.com/ApXZpI0.png)
![](https://i.imgur.com/jha3hU7.png)
![](https://i.imgur.com/UIcnsZb.png)

> 查询是新建一个搜索的activity然后进行判断，再动态地显示出来

    public boolean onQueryTextChange(String newText) {
        String selection = NotePad.Notes.COLUMN_NAME_TITLE + " Like ? ";
        String[] selectionArgs = { "%"+newText+"%" };
        Cursor cursor = managedQuery(
                getIntent().getData(),
                PROJECTION,
                selection,
                selectionArgs,
                NotePad.Notes.DEFAULT_SORT_ORDER
        );
        String[] dataColumns = { NotePad.Notes.COLUMN_NAME_TITLE ,  NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE };
        int[] viewIDs = { android.R.id.text1 , R.id.text1_time };
        SimpleCursorAdapter adapter = new SimpleCursorAdapter(
                this,
                R.layout.noteslist_item,
                cursor,
                dataColumns,
                viewIDs
        );
        setListAdapter(adapter);
        return true;
    }
附加功能
--

>  - UI美化

        UI美化主要是让整体界面看得更加友好如下图

![](https://i.imgur.com/2epBK7a.png)
![](https://i.imgur.com/ApXZpI0.png)

>  -笔记排序
用户可以根据创建时间和修改时间两个方面来进行排序
![](https://i.imgur.com/2epBK7a.png)
![](https://i.imgur.com/4MihK2z.png)

> 排序主要在NoteList菜单switch下添加case

    case R.id.menu_sortr:
                cursor = managedQuery(
                        getIntent().getData(),
                        PROJECTION,
                        null,
                        null,
                        NotePad.Notes._ID
                );
                adapter = new SimpleCursorAdapter(
                        this,
                        R.layout.noteslist_item,
                        cursor,
                        dataColumns,
                        viewIDs
                );
                setListAdapter(adapter);
                return true;

            case R.id.menu_sortd:
                cursor = managedQuery(
                        getIntent().getData(),
                        PROJECTION,
                        null,
                        null,
                        NotePad.Notes.DEFAULT_SORT_ORDER
                );
                adapter = new SimpleCursorAdapter(
                        this,
                        R.layout.noteslist_item,
                        cursor,
                        dataColumns,
                        viewIDs
                );
                setListAdapter(adapter);
                return true;
       



感谢观看
====

`




 



