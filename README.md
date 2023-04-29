# PHPMultiLevelDropdownMenu
Fetch dynamic multilevel dropdown menu

Have table column with id, class, menu, parent_id
<br />id int
<br />class string 
<br />menu text ( can store HTML )
<br />parent_id

```PHP
 // Database pretending 
 $rows = [

   ['id' => 1 , 'class' => '', 'menu' => 'menu 1', 'p_id' => 0],
   ['id' => 2 , 'class' => '', 'menu' => '<h1> This is test</h1>', 'p_id' => 0], 
   ['id' => 3 , 'class' => '', 'menu' => 'menu 3', 'p_id' => 0],
   ['id' => 4 , 'class' => '', 'menu' => 'menu 4', 'p_id' => 0], 
   ['id' => 5 , 'class' => '', 'menu' => 'menu 1', 'p_id' => 1],
   ['id' => 6 , 'class' => '', 'menu' => 'menu 2', 'p_id' => 2], 
   ['id' => 7 , 'class' => '', 'menu' => 'menu 3', 'p_id' => 5],
   ['id' => 8 , 'class' => '', 'menu' => 'menu 4', 'p_id' => 7], 

 ];
 
// echo "<pre>";
// var_dump($rows);
// echo "</pre>";

```

```PHP
$items = $rows;
$id = '';

echo "<ul class='md'>";
foreach ($items as $item ) {

    if( $item['p_id'] == 0 ) {

         echo "<li id='".trim(str_replace(' ','',$item['menu'])).'_'.$item['id']."'> <a href='#'> " . $item['menu'] . "</a>";
         $id = $item['id'];
         sub($items, $id);
         echo "</li>";
    }
}

echo "</ul>";
function sub($items, $id) {

    echo "<ul>";
    foreach ($items as $item) {
        
        if( $item['p_id'] == $id ) {

            echo "<li id='".trim(str_replace(' ','',$item['menu'])).'_'.$item['id']."'> <a href='#'> " . $item['menu'] . "</a>";
            sub($items, $item['id']);
            echo "</li>";
            
       }
    }
   echo "</ul>";
}

```
