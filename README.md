import React, { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { Button } from "@/components/ui/button";

export default function BMICalculator() {
  const [weight, setWeight] = useState("");
  const [height, setHeight] = useState("");
  const [bmi, setBmi] = useState(null);
  const [category, setCategory] = useState("");

  const calculateBMI = () => {
    const w = parseFloat(weight);
    const h = parseFloat(height) / 100;

    if (!w || !h || w <= 0 || h <= 0) {
      setBmi(null);
      setCategory("Please enter valid values.");
      return;
    }

    const bmiValue = w / (h * h);
    setBmi(bmiValue.toFixed(2));

    if (bmiValue < 18.5) setCategory("Underweight");
    else if (bmiValue < 24.9) setCategory("Normal weight");
    else if (bmiValue < 29.9) setCategory("Overweight");
    else setCategory("Obese");
  };

  const reset = () => {
    setWeight("");
    setHeight("");
    setBmi(null);
    setCategory("");
  };

  return (
    <div className="min-h-screen bg-gradient-to-br from-blue-100 to-purple-200 flex items-center justify-center p-4">
      <Card className="w-full max-w-md shadow-2xl rounded-2xl p-6 bg-white">
        <CardContent className="space-y-4">
          <h1 className="text-2xl font-bold text-center text-gray-800">BMI Calculator</h1>
          
          <div className="space-y-2">
            <label className="text-sm text-gray-600">Weight (kg)</label>
            <Input
              type="number"
              value={weight}
              onChange={(e) => setWeight(e.target.value)}
              placeholder="e.g. 70"
              className="rounded-xl"
            />
          </div>

          <div className="space-y-2">
            <label className="text-sm text-gray-600">Height (cm)</label>
            <Input
              type="number"
              value={height}
              onChange={(e) => setHeight(e.target.value)}
              placeholder="e.g. 170"
              className="rounded-xl"
            />
          </div>

          <div className="flex gap-4">
            <Button onClick={calculateBMI} className="w-full rounded-xl">Calculate</Button>
            <Button onClick={reset} variant="secondary" className="w-full rounded-xl">Reset</Button>
          </div>

          {bmi && (
            <div className="text-center mt-4">
              <p className="text-lg font-semibold">Your BMI: <span className="text-blue-600">{bmi}</span></p>
              <p className="text-sm text-gray-600">Category: <span className="font-medium">{category}</span></p>
            </div>
          )}

          {!bmi && category && (
            <p className="text-center text-red-500 text-sm">{category}</p>
          )}
        </CardContent>
      </Card>
    </div>
  );
}
