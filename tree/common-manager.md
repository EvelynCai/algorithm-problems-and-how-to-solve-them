---
description: Amazon
---

# Lowest Common Manager

### 1. Problem: 

一个公司的级别树，最上面是CEO。

如果employee下面有需要向他report的人的话，这个employee 就是manager，每个employee 最多有一个manager。

Employee结构如下：

```text
class Employee { 
    int id; 
    List reports = new ArrayList(); 
    public void setId(int val){ 
        id = val; 
    } 
    
    public int getId(){ 
        return id; 
    } 
    
    public void addReport(Employee emp){ 
        reports.add(emp); 
    } 
    
    public List getReports(){ 
        return reports; 
    }
}
```

input: 两个employee 

output: 找出他们的最低的common manager。

**Assumptions：**

* ceo is not a manager -&gt; if LCA == ceo -&gt; return null 
* employee may not in the company -&gt; return null



### 2. JAVA Implementation

```text
public class CommonManager {
    public Employee comManager (Employee ceo, Employee emp1, Employee emp2){
        if (ceo == null || ceo == emp1 || ceo == emp2) {
            return null;
        }
        
        Employee result = findLCM(ceo, emp1, emp2);
        return result == ceo ? null : result;
    }
    
    private Employee findLCM(Employee manager, Employee e1, Employee e2) {
        // base case: hit bottom or find one of the targets
        if (manager == null || manger == e1 || manger == e2) {
            return manager;
        }
        
        // recursion
        for (Employee sub: manger.getReports()) {
            Employee found = findLCM(sub, e1, e2);
            if (found != null) {
                Employee target = found == e1 ? e2 : e1;
                boolean contains = search(found, target);
                return contains ? found : null;
            }
        }       
        
        return null;        
    }
    
    private boolean search(Employee root, Employee target) {
        if (root == null) {
            return false;
        }
        
        if (root == target) {
            return true;
        }
        
        for (Employee child: root.getReports()) {
            boolean tmp = search(child, target);
            if (tmp) {
                return true;
            }
        }
        
        return false;
    }
}
```



