export function getImageDimensions(data) {
  if (data[0] === 137 && data[1] === 80 && data.length >= 24) {
    const width = new DataView(data.buffer, data.byteOffset + 16).getUint32(0, false);
    const height = new DataView(data.buffer, data.byteOffset + 20).getUint32(0, false);
    return { width, height };
  }
  if (data[0] === 255 && data[1] === 216) {
    let i = 2;
    while (i < data.length - 8) {
      if (data[i] === 255) {
        const marker = data[i + 1];
        if (marker >= 192 && marker <= 195 || marker === 201) {
          const height = data[i + 5] << 8 | data[i + 6];
          const width = data[i + 7] << 8 | data[i + 8];
          return { width, height };
        }
        const len = data[i + 2] << 8 | data[i + 3];
        i += len + 2;
      } else {
        i++;
      }
    }
  }
  if (data[0] === 71 && data[1] === 73 && data[2] === 70 && data.length >= 10) {
    const width = data[6] | data[7] << 8;
    const height = data[8] | data[9] << 8;
    return { width, height };
  }
  return {};
}
