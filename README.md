# Test Task


### Задача 1.1

```
SELECT u1.id, u1.name
FROM users u1
JOIN users u2 ON u1.invited_by_user_id = u2.id
WHERE u1.posts_qty > u2.posts_qty;
```

### Задача 1.2

```
SELECT u.id, name, u.group_id, MAX(u.posts_qty) AS max_posts_qty
FROM users u
JOIN (
    SELECT group_id, MAX(posts_qty) AS max_posts_qty_per_group
    FROM users
    GROUP BY group_id
) AS max_per_group
ON u.group_id = max_per_group.group_id AND u.posts_qty = max_per_group.max_posts_qty_per_group
GROUP BY u.id, u.name, u.group_id;

Задача 1.3

SELECT g.group_id, g.name, COUNT(u.id) AS user_count
FROM groups g
JOIN users u ON g.id = u.group_id
GROUP BY g.id, g.name
HAVING COUNT(u.id) > 10000;
```

### Задача 1.4

```
SELECT u.id, u.name, u.group_id
FROM users u
JOIN users inviting_user ON u.invited_by_user_id = inviting_user.id
WHERE u.group_id != inviting_user.group_id;  Задача 1.5  SELECT group_id, COUNT(*) AS post_count
FROM users
GROUP BY group_id
HAVING COUNT(*) = (
    SELECT COUNT(*) AS max_post_count
    FROM users
    GROUP BY group_id
    ORDER BY max_post_count DESC
    LIMIT 1
);
```

### Задача 2

```
function countTuesdaysBetweenDates($start_date, $end_date) {
    // Преобразуем даты в метки времени UNIX
    $start_timestamp = strtotime($start_date);
    $end_timestamp = strtotime($end_date);
    
    // Находим первый вторник после начальной даты
    $first_tuesday = strtotime('next Tuesday', $start_timestamp);
    
    // Находим последний вторник перед конечной датой
    $last_tuesday = strtotime('last Tuesday', $end_timestamp);
    
    // Рассчитываем количество вторников между датами
    $num_tuesdays = ceil(($last_tuesday - $first_tuesday) / (7 * 24 * 60 * 60)) + 1;
    
    // Учитываем возможные крайние случаи
    if (date('N', $start_timestamp) == 2) {
        $num_tuesdays++;
    }
    if (date('N', $end_timestamp) == 2) {
        $num_tuesdays++;
    }
    
    return $num_tuesdays;
}

// Пример использования функции
$start_date = '2024-01-01';
$end_date = '2024-12-31';
echo "Количество вторников между $start_date и $end_date: " . countTuesdaysBetweenDates($start_date, $end_date);
```

### Задача 3

```
class CircularDeque {
    private $deque;
    private $maxSize;
    private $front;
    private $rear;
    private $size;
    
    public function __construct($maxSize) {
        $this->maxSize = $maxSize;
        $this->deque = array_fill(0, $maxSize, null);
        $this->front = 0;
        $this->rear = 0;
        $this->size = 0;
    }
    
    public function pushBack($value) {
        if ($this->size == $this->maxSize) {
            return false;
        }
        
        $this->deque[$this->rear] = $value;
        $this->rear = ($this->rear + 1) % $this->maxSize;
        $this->size++;
        
        return true;
    }
    
    public function pushFront($value) {
        if ($this->size == $this->maxSize) {
            return false;
        }
        
        $this->front = ($this->front - 1 + $this->maxSize) % $this->maxSize;
        $this->deque[$this->front] = $value;
        $this->size++;
        
        return true;
    }
    
    public function popBack() {
        if ($this->isEmpty()) {
            return false;
        }
        
        $this->rear = ($this->rear - 1 + $this->maxSize) % $this->maxSize;
        $value = $this->deque[$this->rear];
        $this->deque[$this->rear] = null;
        $this->size--;
        
        return $value;
    }
    
    public function popFront() {
        if ($this->isEmpty()) {
            return false;
        }
        
        $value = $this->deque[$this->front];
        $this->deque[$this->front] = null;
        $this->front = ($this->front + 1) % $this->maxSize;
        $this->size--;
        
        return $value;
    }
    
    public function isEmpty() {
        return $this->size == 0;
    }
}
```

### Задача 4

```
function sumNeighbors($matrix, $row, $col) {
    $sum = 0;
    $n = count($matrix);
    $m = count($matrix[0]);
    
    // Проверка влево
    if ($col > 0) {
        $sum += $matrix[$row][$col - 1];
    }
    // Проверка вправо
    if ($col < $m - 1) {
        $sum += $matrix[$row][$col + 1];
    }
    // Проверка вверх
    if ($row > 0) {
        $sum += $matrix[$row - 1][$col];
    }
    // Проверка вниз
    if ($row < $n - 1) {
        $sum += $matrix[$row + 1][$col];
    }
    
    return $sum;
}

// Пример использования функции
$matrix = [
   [ 51, 71, 1, 50 ],
    [ 13, 5, 19, 11 ],
    [ 60, 4, 11, 20 ],
    [ 13, 34, 17, 0 ],
    [ 16, 53, 1, 32 ]
];

$row = 1;
$col = 1;
echo "Сумма соседей элемента ($row, $col): " . sumNeighbors($matrix, $row, $col);
```
