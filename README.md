# turtlesim_wasd-controls
This is to change the controls from arrow keys to wasd
#!/usr/bin/env python
# license removed for brevity
import rospy
from geometry_msgs.msg import Twist

def talker():
    pub = rospy.Publisher('turtle1/cmd_vel', Twist, queue_size=10)
    rospy.init_node('talker', anonymous=True)
    rate = rospy.Rate(10) # 10hz
    

    while not rospy.is_shutdown():
        cmnd = raw_input()
        arg = Twist()
        if cmnd == 'w':
            arg.linear.x =  1.0
        elif cmnd == 's':
            arg.linear.x = -1.0
        arg.linear.y = 0
        arg.linear.z = 0
        arg.angular.x = 0
        arg.angular.y = 0
        if cmnd == 'd':
            arg.angular.z = -(80 *3.14)/180
        elif cmnd == 'a':
            arg.angular.z = (80 * 3.14)/180
        rospy.loginfo(arg)
        pub.publish(arg)
        rate.sleep()

if __name__ == '__main__':
    try:
        talker()
    except rospy.ROSInterruptException:
        pass
