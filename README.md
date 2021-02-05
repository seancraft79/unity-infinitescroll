# unity-infinitescroll
Unity Infinite scrollview

## Features
1. Easy, light, mobile-friendly, just one script
2. List items are fully customizable to fit your project
3. Dynamic, data-driven lists
4. Efficient reusing of list items
5. Optional pull-to-refresh function
6. Diffirent list items height/width support!
7. Demos, tutorials and full C# source code are all included

## How to use
1. Copy the files into your existing unity project asset folder
2. Attach ```InfiniteScroll``` script to your Unity UI ```ScrollView``` object
3. Init list and define callbacks
4. Check or Set Editor inspector ```Default Item Rect Pivot``` field to ensure items' position

### Sample Code
```
    private void Awake()
    {
        infiniteScroll = GetComponent<InfiniteScroll>();
        infiniteScroll.OnFill += OnFillItem;
        infiniteScroll.OnHeight += OnHeightItem;
        infiniteScroll.OnWidth += OnWidthItem;
        var prefabSize = UIUtil.GetRectTransformSize(infiniteScroll.Prefab.GetComponent<RectTransform>());
        itemWidth = (int)prefabSize.x;
        itemHeight = (int) prefabSize.y;
    }

    void OnFillItem (int index, GameObject item)
    {
        var rect = item.GetComponent<RectTransform>();
        var osli = item.GetComponent<OfficerSearchListItem>();
        if (osli != null)
        {
            osli.Init(listData[index]);
            osli.OnItemClickListener = OnItemClickListener;
            osli.OnLayoutClickListener = OnLayoutClickListener;

            var itemBg = item.GetComponent<Image>();
            if (index % 2 == 1)
                itemBg.color = listItemOddColor;
            else itemBg.color = listItemDefaultColor;
        }
        else e($"OnFillItem listdata at {index} null");
    }

    int OnHeightItem (int index) {
        return itemHeight;
    }

    int OnWidthItem (int index) {
        return itemWidth;
    }
```