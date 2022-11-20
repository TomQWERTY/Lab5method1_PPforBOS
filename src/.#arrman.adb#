with Ada.Text_IO;
use Ada.Text_IO;

procedure arrman is

   array_size : Integer := 800;
   thread_count : Integer := array_size / 10;

   type my_array is array (1 .. array_size) of Integer;

   a : my_array;

   function part_sum (left : Integer; Right : Integer) return Integer is
      sum : Integer := 0;
      i   : Integer;
   begin
      i := left;
      while i <= Right loop
            sum := sum + a (i);
         i := i + 1;
      end loop;
      return sum;
   end part_sum;

   procedure create_array is
   begin
      for i in a'Range loop
         a (i) := i;
      end loop;
   end create_array;

   task type my_task is
      entry start(left, RigHt : in Integer);
      entry finish(sum1 : out Integer);
   end my_task;



   task body my_task is
      left, RigHt : Integer;
      sum : Integer := 0;

   begin
      accept start(left, RigHt : in Integer) do
         my_task.left := left;
         my_task.right := Right;
      end start;
      sum := part_sum (left, right);
      accept finish (sum1 : out Integer) do
         sum1 := sum;
      end finish;
   end my_task;

   task1 : array(1..thread_count) of my_task;

   part_sums : array(1..thread_count) of Integer;

   sum00 : integer;
begin
   create_array;
   sum00 := 0;
   for i in a'Range loop
      sum00 := sum00 + a(i);
   end loop;

   Put_Line("Single-thread result: " & sum00'img);

   for i in task1'Range loop
      task1(i).start(array_size / thread_count * (i - 1) + 1,
                    array_size / thread_count * i);
      end loop;
   for i in task1'Range loop
      task1(i).finish(sum00);
      part_sums(i) := sum00;
   end loop;
   sum00 := 0;
   for i in part_sums'Range loop
      sum00 := sum00 + part_sums(i);
   end loop;
   Put_Line("Multi-thread result: " & sum00'img);

end arrman;
