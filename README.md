# museum-mission-app
import React, { useState } from "react";
import { View, Text, TouchableOpacity, TextInput, Button, StyleSheet, Alert } from "react-native";

const answers = ["사진", "김벅수", "41", "제주동자석", "신라시대", "1000원", "벽사진경", "흥인군", "길상"];
const missions = [
  "석호 근처에 숨겨진 거울을 찾아 셀카를 찍으세요.",
  "문인석을 찾아 빨간색의 이름을 확인하세요.",
  "승승장구 길 계단 개수를 세어보세요.",
  "동자음악회 앞에서 휘파람을 불고 녹음하세요.",
  "재래식 화장실 천장에 붙어 있는 단어를 확인하세요.",
  "우물 안에 있는 동전의 금액을 확인하세요.",
  "무너진 돌탑을 다시 쌓아 보여주세요.",
  "신도비의 잘못된 단어를 찾으세요.",
  "무병장수 길 시작점에서 저승요원에게 단어를 들으세요."
];

export default function App() {
  const [puzzle, setPuzzle] = useState(Array(9).fill("?"));
  const [selectedMission, setSelectedMission] = useState(null);
  const [input, setInput] = useState("");

  const handleAnswerSubmit = () => {
    if (input.trim() === answers[selectedMission]) {
      const newPuzzle = [...puzzle];
      newPuzzle[selectedMission] = answers[selectedMission]; // 정답 표시
      setPuzzle(newPuzzle);
      setSelectedMission(null);
      setInput("");
    } else {
      Alert.alert("오답입니다!", "다시 시도해보세요.");
    }
  };

  return (
    <View style={styles.container}>
      {!selectedMission ? (
        <View>
          <Text style={styles.title}>수복강녕 미션</Text>
          <View style={styles.puzzleGrid}>
            {puzzle.map((piece, index) => (
              <TouchableOpacity key={index} onPress={() => setSelectedMission(index)} style={styles.puzzlePiece}>
                <Text style={styles.puzzleText}>{piece}</Text>
              </TouchableOpacity>
            ))}
          </View>
        </View>
      ) : (
        <View>
          <Text style={styles.missionText}>{missions[selectedMission]}</Text>
          <TextInput
            placeholder="정답 입력"
            value={input}
            onChangeText={setInput}
            style={styles.input}
          />
          <Button title="정답 제출" onPress={handleAnswerSubmit} />
        </View>
      )}
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    justifyContent: "center",
    padding: 20,
    backgroundColor: "#f5f5f5",
  },
  title: {
    fontSize: 24,
    fontWeight: "bold",
    marginBottom: 20,
    textAlign: "center",
  },
  puzzleGrid: {
    flexDirection: "row",
    flexWrap: "wrap",
    justifyContent: "center",
  },
  puzzlePiece: {
    width: 100,
    height: 100,
    borderWidth: 1,
    margin: 5,
    justifyContent: "center",
    alignItems: "center",
    backgroundColor: "lightgray",
  },
  puzzleText: {
    fontSize: 18,
  },
  missionText: {
    fontSize: 20,
    fontWeight: "bold",
    marginBottom: 10,
    textAlign: "center",
  },
  input: {
    borderWidth: 1,
    padding: 10,
    width: 200,
    textAlign: "center",
    marginBottom: 10,
    backgroundColor: "white",
  },
});
