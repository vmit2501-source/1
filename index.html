import React, { useState, useRef, useEffect, useCallback } from 'react';
import { Upload, Download, Settings, Image as ImageIcon, Move, RotateCcw, ImagePlus, UserCircle, Layers, ZoomIn } from 'lucide-react';

export default function PhotoMerger() {
  const [activeTab, setActiveTab] = useState('user');
  
  // Admin states
  const [templateSrc, setTemplateSrc] = useState(null);
  const [photoCount, setPhotoCount] = useState(1);
  
  // User states
  // Photos state: Array of objects { id, src, scale, x, y }
  const [photos, setPhotos] = useState([{ id: 0, src: null, scale: 1, x: 0, y: 0 }]);
  const [activePhotoId, setActivePhotoId] = useState(0);
  
  // Interaction refs
  const containerRef = useRef(null);
  const isDragging = useRef(false);
  const dragStart = useRef({ x: 0, y: 0 });
  const posStart = useRef({ x: 0, y: 0 });

  // Update photo array when admin changes photo count
  useEffect(() => {
    setPhotos(prev => {
      const newPhotos = [...prev];
      if (photoCount > prev.length) {
        for (let i = prev.length; i < photoCount; i++) {
          newPhotos.push({ id: i, src: null, scale: 1, x: 0, y: 0 });
        }
      } else if (photoCount < prev.length) {
        newPhotos.splice(photoCount);
      }
      return newPhotos;
    });
    
    if (activePhotoId >= photoCount) {
      setActivePhotoId(0);
    }
  }, [photoCount, activePhotoId]);

  // Handle Image Uploads
  const handleTemplateUpload = (e) => {
    const file = e.target.files?.[0];
    if (file) {
      const reader = new FileReader();
      reader.onload = (event) => setTemplateSrc(event.target.result);
      reader.readAsDataURL(file);
    }
  };

  const handlePhotoUpload = (e, id) => {
    const file = e.target.files?.[0];
    if (file) {
      const reader = new FileReader();
      reader.onload = (event) => {
        setPhotos(prev => prev.map(p => 
          p.id === id ? { ...p, src: event.target.result, scale: 1, x: 0, y: 0 } : p
        ));
        setActivePhotoId(id); // Auto-select the newly uploaded photo
      };
      reader.readAsDataURL(file);
    }
  };

  const updateActivePhoto = (updates) => {
    setPhotos(prev => prev.map(p => 
      p.id === activePhotoId ? { ...p, ...updates } : p
    ));
  };

  // Drag and pan logic for the ACTIVE photo
  const handlePointerDown = (e) => {
    const activePhoto = photos.find(p => p.id === activePhotoId);
    if (!activePhoto || !activePhoto.src) return;
    
    isDragging.current = true;
    const clientX = e.touches ? e.touches[0].clientX : e.clientX;
    const clientY = e.touches ? e.touches[0].clientY : e.clientY;
    
    dragStart.current = { x: clientX, y: clientY };
    posStart.current = { x: activePhoto.x, y: activePhoto.y };
  };

  const handlePointerMove = useCallback((e) => {
    if (!isDragging.current) return;
    
    const clientX = e.touches ? e.touches[0].clientX : e.clientX;
    const clientY = e.touches ? e.touches[0].clientY : e.clientY;
    
    const dx = clientX - dragStart.current.x;
    const dy = clientY - dragStart.current.y;
    
    updateActivePhoto({
      x: posStart.current.x + dx,
      y: posStart.current.y + dy
    });
  }, [activePhotoId, photos]); // Need dependencies to access latest state

  const handlePointerUp = useCallback(() => {
    isDragging.current = false;
  }, []);

  useEffect(() => {
    window.addEventListener('mousemove', handlePointerMove);
    window.addEventListener('mouseup', handlePointerUp);
    window.addEventListener('touchmove', handlePointerMove, { passive: false });
    window.addEventListener('touchend', handlePointerUp);
    
    return () => {
      window.removeEventListener('mousemove', handlePointerMove);
      window.removeEventListener('mouseup', handlePointerUp);
      window.removeEventListener('touchmove', handlePointerMove);
      window.removeEventListener('touchend', handlePointerUp);
    };
  }, [handlePointerMove, handlePointerUp]);

  // Export Logic using HTML5 Canvas
  const exportImage = async () => {
    if (!templateSrc || !containerRef.current) return;

    const loadImg = (src) => new Promise((resolve, reject) => {
      if (!src) return resolve(null);
      const img = new Image();
      img.onload = () => resolve(img);
      img.onerror = reject;
      img.src = src;
    });

    try {
      const templateImg = await loadImg(templateSrc);
      const canvas = document.createElement('canvas');
      canvas.width = templateImg.naturalWidth;
      canvas.height = templateImg.naturalHeight;
      const ctx = canvas.getContext('2d');

      const container = containerRef.current;
      const multiplier = canvas.width / container.offsetWidth;

      // Draw all uploaded photos
      for (const photo of photos) {
        if (!photo.src) continue;
        const photoImg = await loadImg(photo.src);
        
        const drawnPhotoWidth = canvas.width * photo.scale;
        const photoAspectRatio = photoImg.naturalHeight / photoImg.naturalWidth;
        const drawnPhotoHeight = canvas.width * photoAspectRatio * photo.scale;

        const drawX = photo.x * multiplier;
        const drawY = photo.y * multiplier;

        ctx.drawImage(photoImg, drawX, drawY, drawnPhotoWidth, drawnPhotoHeight);
      }

      // Draw template on top
      ctx.drawImage(templateImg, 0, 0, canvas.width, canvas.height);

      // Trigger Download
      const dataUrl = canvas.toDataURL('image/png', 1.0);
      const link = document.createElement('a');
      link.download = 'vk-merged-photo.png';
      link.href = dataUrl;
      link.click();
    } catch (err) {
      console.error('Error generating image', err);
    }
  };

  const activePhoto = photos.find(p => p.id === activePhotoId);
  const allPhotosUploaded = photos.every(p => p.src !== null);

  return (
    <div className="min-h-screen bg-[#EBEDF0] text-[#000000] font-sans pb-12">
      {/* Header (VK-like styling) */}
      <header className="bg-white shadow-sm sticky top-0 z-50">
        <div className="max-w-5xl mx-auto px-4 h-14 flex justify-between items-center">
          <div className="flex items-center gap-2">
            <div className="w-8 h-8 bg-[#0077FF] rounded-lg flex items-center justify-center">
              <ImagePlus className="w-5 h-5 text-white" />
            </div>
            <h1 className="text-lg font-semibold text-gray-900">VK Photo Tool</h1>
          </div>
          
          <div className="flex bg-gray-100 p-1 rounded-lg">
            <button
              onClick={() => setActiveTab('user')}
              className={`flex items-center gap-1.5 px-3 py-1.5 rounded-md text-sm font-medium transition-colors ${
                activeTab === 'user' ? 'bg-white shadow-sm text-[#0077FF]' : 'text-gray-500 hover:text-gray-700'
              }`}
            >
              <UserCircle className="w-4 h-4" />
              <span className="hidden sm:inline">User Mode</span>
            </button>
            <button
              onClick={() => setActiveTab('admin')}
              className={`flex items-center gap-1.5 px-3 py-1.5 rounded-md text-sm font-medium transition-colors ${
                activeTab === 'admin' ? 'bg-white shadow-sm text-[#0077FF]' : 'text-gray-500 hover:text-gray-700'
              }`}
            >
              <Settings className="w-4 h-4" />
              <span className="hidden sm:inline">Admin</span>
            </button>
          </div>
        </div>
      </header>

      <main className="max-w-5xl mx-auto px-4 mt-6">
        
        {/* ADMIN TAB */}
        {activeTab === 'admin' && (
          <div className="max-w-xl mx-auto bg-white p-6 rounded-2xl shadow-sm animate-in fade-in zoom-in-95 duration-200">
            <div className="mb-6">
              <h2 className="text-xl font-semibold mb-1">Admin Settings</h2>
              <p className="text-gray-500 text-sm">Configure the template and required number of photos.</p>
            </div>
            
            <div className="space-y-6">
              {/* Photo Count Setup */}
              <div>
                <label className="block text-sm font-medium text-gray-700 mb-2">Number of Photos in Template</label>
                <div className="flex items-center gap-4">
                  <input 
                    type="range" 
                    min="1" 
                    max="5" 
                    value={photoCount} 
                    onChange={(e) => setPhotoCount(parseInt(e.target.value))}
                    className="flex-1 h-2 bg-gray-200 rounded-lg appearance-none cursor-pointer accent-[#0077FF]"
                  />
                  <span className="font-semibold text-lg w-8 text-center text-[#0077FF] bg-blue-50 py-1 rounded-md">{photoCount}</span>
                </div>
              </div>

              {/* Template Upload */}
              <div>
                <label className="block text-sm font-medium text-gray-700 mb-2">Upload Template (Transparent PNG)</label>
                <label className="flex flex-col items-center justify-center w-full h-48 border-2 border-dashed border-blue-200 rounded-xl bg-blue-50/30 hover:bg-blue-50/80 cursor-pointer transition-colors group relative overflow-hidden">
                  {templateSrc ? (
                    <img src={templateSrc} alt="Template" className="absolute inset-0 w-full h-full object-contain p-4 opacity-40 group-hover:opacity-20 transition-opacity" />
                  ) : null}
                  <div className="flex flex-col items-center justify-center pt-5 pb-6 relative z-10">
                    <Upload className="w-8 h-8 text-[#0077FF] mb-2 group-hover:-translate-y-1 transition-transform" />
                    <p className="text-sm text-gray-700 font-medium">Click to upload template</p>
                    <p className="text-xs text-gray-500 mt-1">PNG with transparency</p>
                  </div>
                  <input type="file" className="hidden" accept="image/png" onChange={handleTemplateUpload} />
                </label>
              </div>
            </div>
          </div>
        )}

        {/* USER TAB */}
        {activeTab === 'user' && (
          <div className="grid grid-cols-1 lg:grid-cols-12 gap-6 animate-in fade-in zoom-in-95 duration-200">
            
            {/* Left Column: Controls */}
            <div className="lg:col-span-4 space-y-4">
              
              {/* 1. Upload Photos */}
              <div className="bg-white p-5 rounded-2xl shadow-sm">
                <h3 className="text-md font-semibold mb-3 flex items-center gap-2">
                  <ImageIcon className="w-4 h-4 text-[#0077FF]" />
                  1. Upload Photos ({photos.filter(p => p.src).length}/{photoCount})
                </h3>
                
                <div className="grid grid-cols-2 gap-3">
                  {photos.map((photo, index) => (
                    <label 
                      key={photo.id}
                      className={`flex flex-col items-center justify-center h-24 border-2 rounded-xl cursor-pointer transition-all ${
                        photo.src 
                          ? (activePhotoId === photo.id ? 'border-[#0077FF] bg-blue-50 ring-2 ring-[#0077FF]/20' : 'border-gray-200 bg-gray-50 hover:bg-gray-100')
                          : 'border-dashed border-gray-300 bg-gray-50 hover:border-[#0077FF]/50 hover:bg-blue-50/30'
                      }`}
                      onClick={(e) => {
                        if (photo.src) {
                          e.preventDefault(); // Prevent file dialog if already uploaded, just select it
                          setActivePhotoId(photo.id);
                        }
                      }}
                    >
                      {photo.src ? (
                        <div className="relative w-full h-full p-1">
                          <img src={photo.src} alt={`Slot ${index + 1}`} className="w-full h-full object-cover rounded-lg" />
                          <div className="absolute inset-0 bg-black/40 rounded-lg flex items-center justify-center opacity-0 hover:opacity-100 transition-opacity">
                            <span className="text-white text-xs font-medium">Click to edit</span>
                          </div>
                          {activePhotoId === photo.id && (
                            <div className="absolute -top-2 -right-2 bg-[#0077FF] text-white text-[10px] px-2 py-0.5 rounded-full font-bold shadow-sm">
                              Active
                            </div>
                          )}
                        </div>
                      ) : (
                        <div className="flex flex-col items-center text-gray-500">
                          <Upload className="w-5 h-5 mb-1" />
                          <span className="text-xs font-medium">Slot {index + 1}</span>
                        </div>
                      )}
                      {/* Only show file input if no photo uploaded or clicking a specific button to replace (handled loosely here) */}
                      {!photo.src && <input type="file" className="hidden" accept="image/*" onChange={(e) => handlePhotoUpload(e, photo.id)} />}
                    </label>
                  ))}
                </div>
              </div>

              {/* 2. Adjust Active Photo */}
              <div className={`bg-white p-5 rounded-2xl shadow-sm transition-opacity ${!activePhoto?.src ? 'opacity-50 pointer-events-none' : ''}`}>
                <div className="flex justify-between items-center mb-4">
                  <h3 className="text-md font-semibold flex items-center gap-2">
                    <Move className="w-4 h-4 text-[#0077FF]" />
                    2. Adjust Photo {activePhotoId + 1}
                  </h3>
                  <button 
                    onClick={() => updateActivePhoto({ scale: 1, x: 0, y: 0 })}
                    className="text-xs flex items-center gap-1 text-gray-500 hover:text-gray-800 bg-gray-100 px-2 py-1 rounded-md transition-colors"
                  >
                    <RotateCcw className="w-3 h-3" /> Reset
                  </button>
                </div>
                
                <div className="space-y-5">
                  <div>
                    <div className="flex justify-between text-sm text-gray-600 mb-2">
                      <span className="flex items-center gap-1"><ZoomIn className="w-4 h-4"/> Zoom</span>
                      <span className="font-medium">{Math.round((activePhoto?.scale || 1) * 100)}%</span>
                    </div>
                    <input
                      type="range"
                      min="0.1"
                      max="3"
                      step="0.05"
                      value={activePhoto?.scale || 1}
                      onChange={(e) => updateActivePhoto({ scale: parseFloat(e.target.value) })}
                      className="w-full h-2 bg-gray-200 rounded-lg appearance-none cursor-pointer accent-[#0077FF]"
                    />
                  </div>
                  <div className="p-3 bg-blue-50/50 border border-blue-100 rounded-xl text-xs text-gray-600 flex gap-2">
                    <Move className="w-4 h-4 flex-shrink-0 text-[#0077FF]" />
                    <p>Click and drag inside the preview area to move <strong>Photo {activePhotoId + 1}</strong>.</p>
                  </div>
                </div>
              </div>

              {/* 3. Finish */}
              <div className="bg-white p-5 rounded-2xl shadow-sm">
                <h3 className="text-md font-semibold mb-3">3. Finish</h3>
                <button
                  onClick={exportImage}
                  disabled={!templateSrc || !allPhotosUploaded}
                  className="w-full py-3 px-4 bg-[#0077FF] hover:bg-[#0066eb] active:bg-[#0055c4] text-white rounded-xl font-medium shadow-sm transition-all flex justify-center items-center gap-2 disabled:opacity-50 disabled:cursor-not-allowed"
                >
                  <Download className="w-5 h-5" />
                  Save & Download
                </button>
                {(!templateSrc || !allPhotosUploaded) && (
                  <p className="text-[11px] text-center text-red-500 mt-2 font-medium">
                    {!templateSrc ? 'Admin must upload a template first.' : `Please upload all ${photoCount} photos.`}
                  </p>
                )}
              </div>
            </div>

            {/* Right Column: Preview Area */}
            <div className="lg:col-span-8">
              <div className="bg-white p-4 rounded-2xl shadow-sm min-h-[500px] flex flex-col h-full">
                <div className="flex justify-between items-center mb-4 px-2">
                  <h3 className="text-md font-semibold flex items-center gap-2">
                    <Layers className="w-4 h-4 text-gray-500" /> Preview
                  </h3>
                  {activePhoto?.src && (
                    <span className="text-xs font-medium px-2 py-1 bg-blue-50 text-[#0077FF] rounded-md">
                      Editing Photo {activePhotoId + 1}
                    </span>
                  )}
                </div>
                
                <div className="flex-1 w-full bg-[#f0f2f5] rounded-xl overflow-hidden flex items-center justify-center relative custom-checkered-bg border border-gray-100">
                  
                  {/* CSS for checkered background to show transparency */}
                  <style dangerouslySetInnerHTML={{__html: `
                    .custom-checkered-bg {
                      background-image: 
                        linear-gradient(45deg, #e5e7eb 25%, transparent 25%), 
                        linear-gradient(-45deg, #e5e7eb 25%, transparent 25%), 
                        linear-gradient(45deg, transparent 75%, #e5e7eb 75%), 
                        linear-gradient(-45deg, transparent 75%, #e5e7eb 75%);
                      background-size: 20px 20px;
                      background-position: 0 0, 0 10px, 10px -10px, -10px 0px;
                    }
                  `}} />

                  {!templateSrc ? (
                    <div className="text-center p-6 bg-white/90 rounded-2xl shadow-sm m-4 max-w-sm">
                      <Settings className="w-8 h-8 text-gray-300 mx-auto mb-3" />
                      <p className="text-gray-600 text-sm">No template has been set up yet.</p>
                      <button onClick={() => setActiveTab('admin')} className="text-[#0077FF] text-sm mt-3 font-medium hover:underline">Switch to Admin Mode</button>
                    </div>
                  ) : (
                    /* The actual interactive container */
                    <div 
                      ref={containerRef}
                      className="relative w-full max-w-full overflow-hidden shadow-lg touch-none select-none bg-white/20"
                      onMouseDown={handlePointerDown}
                      onTouchStart={handlePointerDown}
                      style={{ cursor: activePhoto?.src ? 'grab' : 'default' }}
                    >
                      {/* User Photos (Bottom Layers) */}
                      {photos.map(photo => {
                        if (!photo.src) return null;
                        return (
                          <img 
                            key={photo.id}
                            src={photo.src} 
                            alt={`Upload ${photo.id}`} 
                            className={`absolute top-0 left-0 w-full h-auto origin-top-left transition-opacity duration-200 ${photo.id === activePhotoId ? 'opacity-100 z-0' : 'opacity-90 z-0'}`}
                            style={{
                              transform: `translate(${photo.x}px, ${photo.y}px) scale(${photo.scale})`,
                              willChange: 'transform'
                            }}
                            draggable={false}
                          />
                        );
                      })}

                      {/* Admin Template (Top Layer) - Pointer events none so we can drag the photos underneath */}
                      <img 
                        src={templateSrc} 
                        alt="Template Overlay" 
                        className="relative w-full h-auto block pointer-events-none drop-shadow-sm"
                        style={{ zIndex: 10 }}
                        draggable={false}
                      />
                    </div>
                  )}
                </div>
              </div>
            </div>
            
          </div>
        )}

      </main>
    </div>
  );
}