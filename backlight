#!/usr/bin/env python

import sys

class Backlight:
    def __init__(self):
        with open("/sys/class/backlight/intel_backlight/max_brightness") as f:
            self._max_brightness = int(f.read())
        with open("/sys/class/backlight/intel_backlight/actual_brightness") as f:
            self._current_brightness = int(f.read())

        if self._max_brightness == 0:
            raise RuntimeError("System max brightness is zero")

        self._percentage = self._current_brightness / self._max_brightness * 100

    def set(self, percentage):
        if(percentage > 100):
            percentage = 100
        elif(percentage <= 0):
            percentage = 1
        value = int(percentage / 100 * self._max_brightness)
        with open("/sys/class/backlight/intel_backlight/brightness", "w") as f:
            f.write(str(value))

    def get(self):
        return self._percentage

def main():
    try:
        usage = "<set/inc/dec> <percentage>"
        if(len(sys.argv) !=  3):
            raise RuntimeError(usage)

        backlight = Backlight()
        command = sys.argv[1]
        val = int(sys.argv[2])
        if(command == "set"):
            backlight.set(val)
        elif(command == "inc"):
            backlight.set(backlight.get() + val)
        elif(command == "dec"):
            backlight.set(backlight.get() - val)
        else:
            raise RuntimeError(usage)
        exit(0)
    except Exception as e:
        print(e)
        exit(1)

if __name__ == "__main__":
    main()
