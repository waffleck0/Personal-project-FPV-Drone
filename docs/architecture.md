#PHASE 1 MATHS CHEAT SHEET — DRONE STABILISATION (ARDUINO)

##This cheat sheet covers the essential maths needed for Phase 1 of your stabilised drone controller project:

-IMU angle estimation
-Gyro integration
-Complementary filtering
-PID control
-Timing (dt)
-Basic algebra for motor mixing
-No advanced maths required.

##ACCELEROMETER → ANGLE (TRIGONOMETRY)

Accelerometer gives:
ax, ay, az

Pitch (rotation around Y-axis):
pitch = arctan( ax / sqrt(ay² + az²) )

Roll (rotation around X-axis):
roll = arctan( ay / sqrt(ax² + az²) )

###Notes:

Use atan2() in code.

Angles usually in radians.

##GYROSCOPE → ANGLE (INTEGRATION)

Gyro gives angular velocity:
omega (deg/s or rad/s)

Angle from gyro:
gyro_angle = previous_angle + omega * dt

dt = time between IMU readings (typically 1–5 ms)

##COMPLEMENTARY FILTER (FUSING GYRO + ACCEL)

theta = alpha * (gyro_angle) + (1 - alpha) * (acc_angle)

alpha is usually between 0.95 and 0.99.

Gyro = smooth but drifts
Accelerometer = noisy but stable
Complementary filter = blends both

##PID CONTROL (STABILISATION)

Error:
e = target_angle - measured_angle

P-term:
P = Kp * e

I-term:
I = previous_I + e * dt

D-term:
D = (e - previous_e) / dt

Output:
u = P + I + D

###Notes:

Tune P first, then D, then I last.

Keep I small.

TIMING (dt)

dt = current_time - previous_time

Used for:

Gyro integration

PID derivative

Complementary filter stability

Typical dt:
0.001–0.005 seconds

BASIC ALGEBRA (MOTOR MIXING)

For quadcopter in X configuration:

motor1 = T + P + R
motor2 = T + P - R
motor3 = T - P - R
motor4 = T - P + R

T = throttle
P = pitch correction
R = roll correction
