##React Hook

- Dưới đây em có demo 1 app đếm số có sử dụng 1 số react hook: 
	+ useState để lấy giá trị đếm ban đầu
	+ useRef để lấy giá trị trước đó
	+ useCallback cho hàm cộng và reset 
	+ useEffect để thay đổi giá trị prevCount sau khi cộng

```javascript
const demoHook = () => {
  const [count, setCount] = useState(0);

  const prevCount = useRef(count);

  const handlePlus = useCallback(() => {
    return setCount(x => x + 1);
  }, []);

  const handleReset = useCallback(() => {
    return setCount(x => (x = 0)), (prevCount.current = 0);
  }, []);

  useEffect(() => {
    prevCount.current = count;
  }, [count]);

  return (
    <View>
      <Text>Previous:{prevCount.current}</Text>
      <Text>Current:{count}</Text>
      <TouchableOpacity
        onPress={handlePlus}
        style={{width: 100, height: 30, backgroundColor: 'red'}}>
        <Text>INCREAMENT</Text>
      </TouchableOpacity>
      <TouchableOpacity
        onPress={handleReset}
        style={{width: 100, height: 30, backgroundColor: 'blue'}}>
        <Text>RESET</Text>
      </TouchableOpacity>
    </View>
  );
};

export const DemoHook = memo(demoHook);
```