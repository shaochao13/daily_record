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