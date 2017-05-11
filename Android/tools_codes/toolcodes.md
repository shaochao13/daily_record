1. <div id="alertdialog_code">AlertDialog 使用代码</div>
```java
AlertDialog.Builder dialog = new AlertDialog.Builder(SecondActivity.this);
dialog.setTitle("This is Dialog");
dialog.setMessage("Something important.");
dialog.setCancelable(false);
dialog.setPositiveButton("OK", new DialogInterface.OnClickListener() {
    @Override
    public void onClick(DialogInterface dialog, int which) {
        
    }
});

dialog.setNegativeButton("Cancel", new DialogInterface.OnClickListener() {
    @Override
    public void onClick(DialogInterface dialog, int which) {

    }
});

dialog.show();
```

2. <div id="progressdialog_code">ProgressDialog 使用代码</div>
```java
button2.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                ProgressDialog progressDialog = new ProgressDialog(MainActivity.this);
                progressDialog.setTitle("This is ProgressDialog");
                progressDialog.setMessage("Loading...");
                progressDialog.setCancelable(true);
                progressDialog.show();

            }
        });
```

3. <div id="hide_actionbar_code">隐藏掉系统自带的标题栏</div>
```java
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    ActionBar actionBar = getSupportActionBar();
    if (actionBar != null){
        actionBar.hide();
    }
}
```