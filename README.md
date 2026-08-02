# อธิบายอัลกอริทึม

## ตัวที่ 1 Recursive Algorithm
 โดยองค์ประกอบหลักมี 2 ส่วนคือ Base Case (เงื่อนไขหยุด) และ Recursive Step (การเรียกซ้ำ)
เเนวคิด: ใช้หลักการเรียกซ้ำของ Recursive Step โดยดึงตัวอักษรตัวสุดท้ายของ สตริง ณ ปัจจุบัน นำมาต่อเข้ากับผลลัพธ์ที่ได้จากการเรียกเมธอดตัวเองซ้ำ โดยส่งสตริงส่วนที่เหลือ (ตำแหน่งแรกถึงตัวก่อนสุดท้าย) ไปประมวลผล
Base Case (เงื่อนไขหยุดการเรียกซ้ำ): เมื่อสตริงมีค่าเป็น null หรือมีความยาวน้อยกว่าหรือเท่ากับ 1 ตัวอักษร

## ตัวที่ 2 Iterative Algorithm 
แนวคิด: ใช้ลูปวนอ่านตัวอักษรของสตริงจากตำแหน่งสุดท้าย (s.length() - 1) ย้อนกลับมายังตำแหน่งแรก (0) และนำตัวอักษรแต่ละตัวมาต่อเข้ากับ StringBuilder ซึ่งเป็นประเภทข้อมูลแบบ Mutable ช่วยให้ไม่สิ้นเปลืองหน่วยความจำ

## Pseudocode
// 1. Recursive Algorithm
Algorithm reverseRecursive(s)
    If s is null or length of s <= 1 Then
        Return s                              // Base Case: หยุดเมื่อข้อความว่างหรือเหลือ 1 ตัว
    End If
    lastChar = character at index (length of s - 1)
    remaining = substring of s from index 0 to (length of s - 2)
    Return lastChar + reverseRecursive(remaining) // Recursive Case: เวียนเกิดกับสตริงส่วนที่เหลือ
End Algorithm

// 2. Iterative Algorithm
Algorithm reverseIterative(s)
    If s is null Then
        Return null
    End If
    Create empty StringBuilder sb
    For i = (length of s - 1) DownTo 0 Do
        Append character at s[i] to sb
    End For
    Return sb.toString()
End Algorithm

## โปรเเกรม Java
public class StringReverser {

    /**
     * อัลกอริทึมที่ 1: Recursive Algorithm
     * Base Case: หากสตริงเป็น null หรือความยาว <= 1 ให้คืนค่ากลับทันที
     * Recursive Case: ดึงตัวอักษรตัวสุดท้าย + เรียกเมธอดซ้ำกับสตริงที่เหลือ
     */
    public static String reverseRecursive(String s) {
        // ตรวจสอบกรณีข้อมูลว่างเพื่อป้องกัน NullPointerException และ StringIndexOutOfBoundsException
        if (s == null || s.length() <= 1) { 
            return s; // Base Case
        }
        // Recursive Case
        return s.charAt(s.length() - 1) + reverseRecursive(s.substring(0, s.length() - 1));
    }

    /**
     * อัลกอริทึมที่ 2: Iterative Algorithm
     * ใช้ลูปอ่านตัวอักษรจากตัวสุดท้ายย้อนกลับมาตัวแรก
     * ใช้ StringBuilder เพื่อหลีกเลี่ยงการสร้าง String Object ใหม่ซ้ำๆ ในหน่วยความจำ
     */
    public static String reverseIterative(String s) {
        if (s == null) {
            return null; // ตรวจสอบกรณีข้อมูลว่าง
        }
        StringBuilder sb = new StringBuilder();
        // อ่านย้อนกลับจากตำแหน่งสุดท้ายลงมายังตำแหน่ง 0
        for (int i = s.length() - 1; i >= 0; i--) {
            sb.append(s.charAt(i));
        }
        return sb.toString();
    }

    public static void main(String[] args) {
        // 1. ทดสอบกรณีข้อมูลปกติ
        String input = "pots&pans";
        System.out.println("Input:  " + input);
        System.out.println("Recursive Output: " + reverseRecursive(input));
        System.out.println("Iterative Output: " + reverseIterative(input));

        // 2. ทดสอบกรณีพิเศษ (Null, สตริงว่าง, สตริง 1 ตัวอักษร)
        System.out.println("\n--- Edge Cases Testing ---");
        System.out.println("Null Input Test:      " + reverseIterative(null));
        System.out.println("Empty String Output:  \"" + reverseIterative("") + "\"");
        System.out.println("Single Char Output:   \"" + reverseIterative("A") + "\"");
    }
}

## ข้อมูลนำเข้า "pots&pans"
## ข้อมูลส่งออก "snap&stop"

# วิเคราะห์ Time Complexity
## อัลกอริทึมที่ 1 (Recursive Algorithm): $O(n^2)$  
เหตุผลสนับสนุน: เมธอดเรียกตัวเองซ้ำจำนวน $n$ ครั้ง (ตามความยาวของสตริง $n$) โดยในทุกๆ 
ครั้งของการเวียนเกิด จะมีการเรียกใช้ substring() ซึ่งมี Time Complexity เป็น $O(n)$ ในการคัดลอกตัวอักษร และใช้เครื่องหมาย + ในการต่อสตริงซึ่งเสียเวลา $O(n)$ ในการสร้างวัตถุ String ใหม่  
ทำให้ได้สมการความสัมพันธ์: $T(n) = T(n-1) + O(n)$ ซึ่งเมื่อแก้สมการจะได้ $O(n^2)$  
## อัลกอริทึมที่ 2 (Iterative Algorithm): $O(n)$  
เหตุผลสนับสนุน: ทำการวนลูปตามความยาวสตริงจำนวน $n$ รอบ โดยการดึงตัวอักษรด้วย charAt() และการต่อตัวอักษรด้วย sb.append() ใช้เวลาคงที่ $O(1)$ ต่อรอบ  
รวมเวลาประมวลผลทั้งหมดเป็น $n \times O(1) = O(n)$  

# วิเคราะห์ Space Complexity
## อัลกอริทึมที่ 1 (Recursive Algorithm): $O(n^2)$  
เหตุผลสนับสนุน: มีการใช้พื้นที่บน Call Stack ลึกสูงสุด $n$ ชั้น และในแต่ละ Call Frame จะมีการสร้าง Object สตริงตัวใหม่จากการใช้ substring() และเครื่องหมาย + ส่งผลให้ใช้พื้นที่หน่วยความจำสะสมรวมเป็น $O(n^2)$
## อัลกอริทึมที่ 2 (Iterative Algorithm): $O(n)$
เหตุผลสนับสนุน: ไม่มีการใช้พื้นที่ Call Stack เพิ่มเติม (Auxiliary Space เพียง $O(1)$) ใช้พื้นที่หน่วยความจำเฉพาะ StringBuilder สำหรับเก็บผลลัพธ์สตริงใหม่ตามขนาดความยาวข้อมูล $n$ ตัวอักษรเท่านั้น

# วิเคราะห์เพิ่มเติมเฉพาะข้อกำหนด
## จำนวนครั้งที่แต่ละอัลกอริทึมประมวลผลตัวอักษร: 
อ่านและประมวลผลตัวอักษร $n$ ครั้งเท่ากัน  
## ผลกระทบจากการต่อสตริงด้วยเครื่องหมาย +: 
เนื่องจาก String ใน Java เป็นประเภท Immutable (ไม่สามารถแก้ไขค่าเดิมได้) การใช้ + จะบังคับให้ JVM สร้างวัตถุ String ชิ้นใหม่และคัดลอกตัวอักษรเดิมมาใส่ทุกครั้ง ส่งผลให้ทำงานช้าลงมาก ($O(n)$ ต่อรอบ) และสร้างขยะในหน่วยความจำ Heap  
## ความแตกต่างระหว่าง String และ StringBuilder: String เป็น Immutable เมื่อเปลี่ยนค่าต้องสร้าง Object ใหม่เสมอ แต่ StringBuilder เป็น Mutable ที่มี Buffer ภายในรองรับการแก้ไขค่าเดิมได้ทันที ทำให้ append() ทำงานได้เร็วด้วยประสิทธิภาพ $O(1)$  
## ผลการทดสอบกับขนาดสตริง ($n = 10, 100, 1,000, 10,000$ ตัวอักษร):  
$n = 10, 100$: ทั้งสองอัลกอริทึมทำงานได้เร็วไม่ต่างกัน  
$n = 1,000$: วิธี Recursive เริ่มช้าอย่างเห็นได้ชัด เนื่องจากผลกระทบของ $O(n^2)$  
$n = 10, 100, 000$: วิธี Recursive เกิดข้อผิดพลาด StackOverflowError หรือ Memory Full เนื่องจากใช้พื้นที่ Call Stack และสร้าง Object มากเกินขีดจำกัดของ JVM ในขณะที่วิธี Iterative สามารถทำงานผ่านได้อย่างรวดเร็ว  

# เปรียบเทียบข้อดี ข้อจำกัด
### 8. การเปรียบเทียบข้อดี ข้อจำกัด และสรุปผล

| ประเด็นการเปรียบเทียบ | อัลกอริทึมที่ 1: Recursive | อัลกอริทึมที่ 2: Iterative |
| :--- | :--- | :--- |
| ข้อดี | โค้ดแสดงโครงสร้างความสัมพันธ์เวียนเกิดชัดเจน | ทำงานรวดเร็ว ใช้หน่วยความจำน้อย มีประสิทธิภาพสูง |
| ข้อจำกัด | สิ้นเปลืองหน่วยความจำ และเสี่ยงต่อ StackOverflowError | ใช้บรรทัดโค้ดมากกว่าวิธีเวียนเกิดเล็กน้อย |
| Time Complexity | O(n^2) | O(n) |
| Space Complexity | O(n^2) | O(n) |

สรุป: Iterative Algorithm เหมาะสมกว่าในทุกเงื่อนไขการใช้งานจริง เนื่องจากมี Time Complexity O(n) และ Space Complexity O(n) ทำงานได้รวดเร็ว ปลอดภัย และไม่เสี่ยงต่อการเกิดข้อผิดพลาดด้านหน่วยความจำเมื่อข้อมูลมีขนาดใหญ่
